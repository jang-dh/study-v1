# 20200624 
The Front-End for wai Framework will be changed to ours 

# Environment Setting

- GitLab

The project was imported to the gradle protect using eclipse.
The well-built check way is to make sure that annotations like @Autowired are enabled.

### Connect Database
src/main/resources/
- dev : development server (together)
- local : development serve (alone) 
- prod : final deploy server 
- uat : test server after developing

### The tomcat build way
In the eclipse, 
1. Double click tomcat -> In the overview tab, 
	open launch configuration - arguments - write `-Dbuildenv=local`

2. If it occur the timeout error, set of the Timeouts to 300 or 500

	
3. In the Modules tab, Edit the web Modules Path to "/" and unchecked Auto reloading enabled 

### Database
In the DBeaver,
1. Right click at database
2. Make hopes and set active
3. Right click at hopes - tools - restore
4. Select the dump file - start

and then you must do this
1. **Authority** : Query = "Grant all privileges on the database database_name to username;"
2. **Default Setting of schema** : Query = "Alter role \<your_login_role> set search_path to hopesadm"

### Live server in VS code
The server for resources.
ex) If you want to open the main.html, you can do that using this without the web server.

settings.json
```json
{

"editor.suggestSelection": "first",

"vsintellicode.modify.editor.suggestSelection": "automaticallyOverrodeDefaultValue",

"java.jdt.ls.vmargs": "-noverify -Xmx1G -XX:+UseG1GC -XX:+UseStringDeduplication -javaagent:\"c:\\Users\\HanaTI\\.vscode\\extensions\\gabrielbb.vscode-lombok-1.0.1\\server\\lombok.jar\"",

"files.exclude": {

"**/.classpath": true,

"**/.project": true,

"**/.settings": true,

"**/.factorypath": true

},

"terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe",

"explorer.confirmDelete": false,

"workbench.iconTheme": "vscode-icons",

"window.zoomLevel": 0,

"javascript.updateImportsOnFileMove.enabled": "always",

"liveServer.settings.multiRootWorkspaceName": "/hopes.view/",

"git.autofetch": true,

"liveServer.settings.donotShowInfoMsg": true,

"git.confirmSync": false,

"java.semanticHighlighting.enabled": true,

"liveServer.settings.AdvanceCustomBrowserCmdLine": "",

"liveServer.settings.ignoreFiles": [

"**"

], // Optional Setting = auto reload when the page is updated and saved

"workbench.colorTheme": "Hopscotch Classic",

"liveServer.settings.ChromeDebuggingAttachment": false

}
```
