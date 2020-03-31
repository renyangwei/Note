- [Room](#room)
  - [导入](#%e5%af%bc%e5%85%a5)
  - [组件](#%e7%bb%84%e4%bb%b6)
    - [DataBase](#database)
    - [Entity](#entity)
    - [DAO](#dao)
  - [版本迁移](#%e7%89%88%e6%9c%ac%e8%bf%81%e7%a7%bb)

# Room

`Room` 在 `SQLite` 上提供了一个抽象层，以便在充分利用 `SQLite` 的强大功能的同时，能够流畅地访问数据库。

## 导入

需要根据实际情况进行选择

```
dependencies {
    def room_version = "2.2.3"

    implementation "androidx.room:room-runtime:$room_version"
    annotationProcessor "androidx.room:room-compiler:$room_version" // For Kotlin use kapt instead of annotationProcessor

      // optional - Kotlin Extensions and Coroutines support for Room
      implementation "androidx.room:room-ktx:$room_version"

      // optional - RxJava support for Room
      implementation "androidx.room:room-rxjava2:$room_version"

      // optional - Guava support for Room, including Optional and ListenableFuture
      implementation "androidx.room:room-guava:$room_version"

      // Test helpers
      testImplementation "androidx.room:room-testing:$room_version"
    }
    
```

## 组件

包含三种：

- DataBase：数据库
- Entity：表结构
- DAO：包含用于访问数据库的方法

### DataBase

1. 自定义类继承 `RoomDatabase`;
2. 将类写成单例模式（推荐）；
3. 写获取 `Dao` 的函数。

举例：

```java
@Database(entities = {Word.class}, version = 1, exportSchema = false)
public abstract class WordDatabase extends RoomDatabase {

    private static WordDatabase instance;

    public static synchronized WordDatabase getInstance(Context context) {
        if (instance == null) {
            instance = Room.databaseBuilder(context.getApplicationContext(), WordDatabase.class, "word_database")
                    .allowMainThreadQueries()
                    .build();
        }
        return instance;
    }

    public abstract WordDao getWordDao();
    // 如果有多个Entities，则增加多个
}
```

### Entity

通过注解与表结构关联。

举例：

```java
@Entity
public class Word {

    @PrimaryKey(autoGenerate = true)
    private int id;

    @ColumnInfo(name = "english_world")
    private String world;

    @ColumnInfo(name = "chinese_meaning")
    private String chineseMeaning;

    public Word(String world, String chineseMeaning) {
        this.world = world;
        this.chineseMeaning = chineseMeaning;
    }

    public String getWorld() {
        return world;
    }

    public void setWorld(String world) {
        this.world = world;
    }

    public String getChineseMeaning() {
        return chineseMeaning;
    }

    public void setChineseMeaning(String chineseMeaning) {
        this.chineseMeaning = chineseMeaning;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }
}
```

### DAO

`DAO` 是一个接口，系统会自动实现。

举例：

```java
@Dao
public interface WordDao {

    @Insert
    void insert(Word... wolds);

    @Delete
    void delete(Word... wolds);

    @Query("DELETE FROM Word")
    void deleteAll();

    @Update
    void update(Word... wolds);

    // 使用LiveData数据结构，系统会自动在其他线程执行
    @Query("SELECT * FROM Word ORDER BY ID DESC")
    LiveData<List<Word>> getAll();
}
```

三个组件都定义好之后我们就可以在 `ViewModule` 中使用了。

```java
public class WordViewModule extends AndroidViewModel {

    private WordRepository repository;

    public WordViewModule(@NonNull Application application) {
        super(application);
        repository = new WordRepository(application);
    }

    public LiveData<List<Word>> getWordListLiveData() {
        return repository.getAll();
    }

    public void insert(Word... words) {
        repository.insert(words);

    }

    public void deleteAll() {
        repository.deleteAll();
    }

}
```

为了让代码封装性更好，我们建立了一个仓库类。

```java
public class WordRepository {

    private WordDao wordDao;

    public WordRepository(Application application) {
        wordDao = WordDatabase.getInstance(application).getWordDao();
    }

    public LiveData<List<Word>> getAll() {
        return wordDao.getAll();
    }

    public void insert(Word... words) {
        new InsertTask(wordDao).execute(words);
    }

    public void deleteAll() {
        new DeleteTask(wordDao).execute();
    }

    static class InsertTask extends AsyncTask<Word, Void, Void> {

        private WordDao wordDao;

        public InsertTask(WordDao wordDao) {
            this.wordDao = wordDao;
        }

        @Override
        protected Void doInBackground(Word... words) {
            wordDao.insert(words);
            return null;
        }
    }

    static class DeleteTask extends AsyncTask<Void, Void, Void> {

        private WordDao wordDao;

        public DeleteTask(WordDao wordDao) {
            this.wordDao = wordDao;
        }

        @Override
        protected Void doInBackground(Void... voids) {
            wordDao.deleteAll();
            return null;
        }
    }

}
```

## 版本迁移

如果要修改表结构，即修改 `Entity` 结构，又不想用户丢失现有的数据，我们可以编写 `Migration` 类。

步骤：
1. 修改 `Entity` 类；
2. 增加 `RoomDatabase` 版本；
3. 编写 `Migration` 类；
4. 设置 `Migration` 类。

举例：

```java
    static final Migration MIGRATION_1_2 = new Migration(1, 2) {
        @Override
        public void migrate(SupportSQLiteDatabase database) {
            // 添加表
            database.execSQL("CREATE TABLE `Fruit` (`id` INTEGER, "
                    + "`name` TEXT, PRIMARY KEY(`id`))");
        }
    };

    static final Migration MIGRATION_2_3 = new Migration(2, 3) {
        @Override
        public void migrate(SupportSQLiteDatabase database) {
            // 增加表字段
            database.execSQL("ALTER TABLE Book "
                    + " ADD COLUMN pub_year INTEGER");
        }
    };

    // 设置 Migration
    Room.databaseBuilder(getApplicationContext(), MyDb.class, "database-name")
            .addMigrations(MIGRATION_1_2, MIGRATION_2_3).build();
    
```

**小技巧**

1. 如果要给组件加上点击效果，我们可以设置：`android:background="?attr/selectableItemBackground"`。
2. 如果要让空间周围也可点击，可以设置 `padding` 值。
3. 分割线有现成的控件可用，其实就是一个View设置为：`android:background="?android:attr/listDivider"` 。
4. 在 `RecycleView` 中设置监听，如果修改了数据，要先将监听设置为null，然后添加数据，最后添加监听，因为 `ViewHolder` 是可回收的。
5. 在 `RecycleView` 中设置监听最好在 `onCreateViewHolder` 中而不是 `onBindViewHolder`，作为性能优化。