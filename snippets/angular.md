# Adding different profiles
To add and run multiple environment profiles in Angular three things are required.
1. A environment ts file
2. Modifying the `angular.json` config file
3. Serving 

## Environment json file
This one is straightfoward, simply add another file to src/environments.
E.g I wanted to add an environment to run the development app from a docker container, so I added the environment `environment.docker.ts`.

## Modifying `angular.json`
To add a new configuration there are 2 places that must be edited.

Under `projects.app_name.configurations`, add a new configuration name and within this configuration add directives to point to the correct environment file.
e.g
```json
          "configurations": {
            "docker": {
              "fileReplacements": [
                {
                  "replace": "src/environments/environment.ts",
                  "with": "src/environments/environment.docker.ts"
                }
                ]
            },
```

Next, we must modify `projects.app_name.serve.configurations`.
Similarly, add another entry for the configuration, this time under `serve`.
```json
          "configurations": {
            "production": {
              "browserTarget": "ng-interview-app:build:production"
            },
             "docker": {
              "browserTarget": "ng-interview-app:build:docker"
            },
          }
```

# Serving
To serve the dev server, use `ng serve -c docker ...`.
Substitute the name `docker` in the command for the name of your configuration.
