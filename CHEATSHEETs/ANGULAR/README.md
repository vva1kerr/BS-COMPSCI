
# `tree -I ".vscode|.git|node_modules"`
```
.
└── camo-brand
    ├── README.md
    ├── angular.json
    ├── package-lock.json
    ├── package.json
    ├── public
    │   └── favicon.ico
    ├── src
    │   ├── app
    │   │   ├── app.config.ts
    │   │   ├── app.css
    │   │   ├── app.html
    │   │   ├── app.routes.ts
    │   │   ├── app.spec.ts
    │   │   └── app.ts
    │   ├── index.html
    │   ├── main.ts
    │   └── styles.css
    ├── tsconfig.app.json
    ├── tsconfig.json
    └── tsconfig.spec.json

5 directories, 18 files
```

# [Angular File Structure](https://v17.angular.io/guide/file-structure)
| Workspace configuration files | Purpose |
| ------------- | ------------- |
| .editorconfig | Configuration for code editors. See EditorConfig. |
| .gitignore | Specifies intentionally untracked files that Git should ignore. |
| README.md | Introductory documentation for the root application. |
| angular.json |  	CLI configuration defaults for all projects in the workspace, including configuration options for build, serve, and test tools that the CLI uses, such as Karma, and Protractor. For details, see Angular Workspace Configuration. |
| package.json | Configures npm package dependencies that are available to all projects in the workspace. See npm documentation for the specific format and contents of this file. |
| package-lock.json | Provides version information for all packages installed into node_modules by the npm client. See npm documentation for details. If you use the yarn client, this file will be yarn.lock instead. |
| src/ | Source files for the root-level application project. |
| node_modules/ | Provides npm packages to the entire workspace. Workspace-wide node_modules dependencies are visible to all projects. |
| tsconfig.json | The base TypeScript configuration for projects in the workspace. All other configuration files inherit from this base file. For more information, see the Configuration inheritance with extends section of the TypeScript documentation. |

# aka
|  |  |
| --- | --- |
| angular.json | Angular workspace config list of execution targets |
| node_modules/ | local repo of node modules |
| package.json | project meta data list of node dependencies |
| src/app/ | app components,templates, etc |
| src/assets/ | images, etc |
| src/environments/ | profiles for environment: dev, test, prod, etc |
| index.html | main launch page |
| polyfills.ts | add supports for different browser versions |
| test.ts | unit test cases |
| tsconfig.json | typescript compiler configs |  
