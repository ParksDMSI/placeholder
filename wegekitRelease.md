## Wedgekit Release instructions
Once you have commited your wedgekit changes to a feature branch, created a pull requet and merged it, it is time to release your changes so that our other repositories can utilize the changes.

#### Release PR instructions
1. Create a release branch from develoop
    1. `git checkout develop`
    2. `git pull`
    3. `git checkout -b release/YYYY-MM-DD.#.#` (the #'s are only for multiple releases in a day)
    4. Please make sure you are in the release branch before proceeding
2. In wedgekit, update the `CHANGELOG.md` for the appropiate package
3. Bump version #'s for your appropiate extension in the `package.json` files
    - A global search for `"@wedgekit/{your component}":` may be helpful to find all instances
4. Create a pull request for the release to master
5. Add git tags to the commit so they can be pushed to the origin
    - `git tag @wedgekit/{package name}@#.#.#` (here the #'s are the most recent release version)
    - `git push origin @wedgekit/{package name}@#.#.#`
6. Merge the release PR

#### Update yarn version #'s
1. Checkout master
    - `git checkout master`
2. Pull to make sure your local instance is up to date
3. Navigate into the package edited
    -   cd packages/{package name}
4. Rebuild yarn and prepare wedgekit for publish
    - `yarn build` and `npm publish`
5. checkout develop and pull
6. Manually merge wedgekit
    -`git merge origin/master`
    -`git push`

#### Update Dependent Repos

##### Agility
1. Checkout develop and pull
2. Checkout a new branch under the name of the feture being added
3. Navigate into the package edited and update the package yarn should reference
    - `yarn add @wedgekit/{package name}`
4. Navigate to the parent agility repo and rerun yarn
    - 'yarn'

##### Storybook
1. Checkout develop and pull
2. Checkout a new branch under the name of the feture being added
3. Update version number in package.json
    -`"wedgekit/{package name}":"{most recent version}"`
4. Navigate into storybook repos
5. Force yarn to rebuild and update it's dependencies to the most current packages
    - `rm -rf node_modules && yarn`
6. Create a PR for the dependency changes
7. ssh into phoenix.dmsi.com
8. Manually pull the most recent version using docker
    - `docker pull dmsi/storybook-public:develop && sudo systemctl stop storybook && sudo systemctl start storybook`

##<span style="color:green">Develop with your new wedgekit changes!</span>
