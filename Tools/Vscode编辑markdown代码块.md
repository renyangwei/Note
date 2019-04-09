# Vscode编辑markdown代码块（snippets）

最近遇到一个问题，用 Vscode 写代码有提示，为什么写 markdown文档没有呢，很不方便。

**文件** > **首选项** > **用户代码片段**，输入 `markdown`，编辑 *markdown.json*：

```
{
	// Place your snippets for markdown here. Each snippet is defined under a snippet name and has a prefix, body and 
	// description. The prefix is what is used to trigger the snippet and the body will be expanded and inserted. Possible variables are:
	// $1, $2 for tab stops, $0 for the final cursor position, and ${1:label}, ${2:another} for placeholders. Placeholders with the 
	// same ids are connected.
	// Example:
	// "Print to console": {
	// 	"prefix": "log",
	// 	"body": [
	// 		"console.log('$1');",
	// 		"$2"
	// 	],
	// 	"description": "Log output to console"
	// }

	"java code": {
		"prefix": "java",
		"body": [
			"```java",
			"$1",
			"```"
		],
		"description": "print java code"
	}
}
```

然后还有最重要的一步

打开 *setting.json*,添加一段：

```json
"[markdown]":  {
    "editor.quickSuggestions": true
  }
```

保存，然后输入 `java` 就可以看到提示了，很 nice!