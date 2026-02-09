## 📦 NPM Commands Cheatsheet

A quick reference for the most common **npm** commands used in modern web development.

---

### npm init [options]
Initializes a new Node.js project and creates a `package.json` file.

| Command | Description | Example |
| -------- | ------------ | -------- |
| `npm init` | Starts interactive project setup. | `npm init` |
| `npm init -y` | Creates `package.json` with default values. | `npm init -y` |

---

### npm install [options]
Installs dependencies into the project.

| Command | Description | Example |
| -------- | ------------ | -------- |
| `npm install` | Installs all dependencies from `package.json`. | `npm install` |
| `npm install [package]` | Installs a package locally. | `npm install axios` |
| `npm install -D [package]` | Installs as dev dependency. | `npm install -D eslint` |
| `npm install -g [package]` | Installs globally. | `npm install -g nodemon` |
| `npm install [package]@version` | Installs specific version. | `npm install react@18` |

---

### npm uninstall [options]
Removes installed dependencies.

| Command | Description | Example |
| -------- | ------------ | -------- |
| `npm uninstall [package]` | Removes a local package. | `npm uninstall axios` |
| `npm uninstall -g [package]` | Removes global package. | `npm uninstall -g nodemon` |
| `npm uninstall -D [package]` | Removes dev dependency. | `npm uninstall -D eslint` |

---

### npm update [options]
Updates installed packages.

| Command | Description | Example |
| -------- | ------------ | -------- |
| `npm update` | Updates all packages. | `npm update` |
| `npm update [package]` | Updates specific package. | `npm update react` |
| `npm update -g` | Updates global packages. | `npm update -g` |

---

### npm outdated [options]
Checks for outdated dependencies.

| Command | Description | Example |
| -------- | ------------ | -------- |
| `npm outdated` | Shows outdated packages. | `npm outdated` |
| `npm outdated -g` | Shows outdated global packages. | `npm outdated -g` |

---

### npm list [options]
Displays installed packages.

| Command | Description | Example |
| -------- | ------------ | -------- |
| `npm list` | Lists local dependencies. | `npm list` |
| `npm list --depth=0` | Lists only top-level packages. | `npm list --depth=0` |
| `npm list -g` | Lists global packages. | `npm list -g` |

---

### npm run [script]
Runs scripts defined in `package.json`.

| Command | Description | Example |
| -------- | ------------ | -------- |
| `npm run` | Shows available scripts. | `npm run` |
| `npm run dev` | Runs `dev` script. | `npm run dev` |
| `npm run build` | Runs `build` script. | `npm run build` |
| `npm start` | Runs `start` script. | `npm start` |
| `npm test` | Runs tests. | `npm test` |

---

### npm audit [options]
Checks for security vulnerabilities.

| Command | Description | Example |
| -------- | ------------ | -------- |
| `npm audit` | Scans for vulnerabilities. | `npm audit` |
| `npm audit fix` | Fixes issues automatically. | `npm audit fix` |
| `npm audit fix --force` | Forces major updates. | `npm audit fix --force` |

---

### npm cache [options]
Manages npm cache.

| Command | Description | Example |
| -------- | ------------ | -------- |
| `npm cache verify` | Verifies cache integrity. | `npm cache verify` |
| `npm cache clean --force` | Clears cache. | `npm cache clean --force` |

---

### npm config [options]
Manages npm configuration.

| Command | Description | Example |
| -------- | ------------ | -------- |
| `npm config list` | Shows config values. | `npm config list` |
| `npm config get registry` | Gets registry URL. | `npm config get registry` |
| `npm config set registry [url]` | Sets registry URL. | `npm config set registry https://registry.npmjs.org/` |

---

### npm info [package]
Displays package information.

| Command | Description | Example |
| -------- | ------------ | -------- |
| `npm info [package]` | Shows package info. | `npm info react` |
| `npm view [package] versions` | Shows all versions. | `npm view react versions` |

---

### npm publish / unpublish
Publishes packages to npm registry.

| Command | Description | Example |
| -------- | ------------ | -------- |
| `npm login` | Logs into npm account. | `npm login` |
| `npm publish` | Publishes package. | `npm publish` |
| `npm unpublish [package]` | Removes published package. | `npm unpublish my-lib` |

---

### npm version [options]
Manages project versioning.

| Command | Description | Example |
| -------- | ------------ | -------- |
| `npm version patch` | Increments patch version. | `npm version patch` |
| `npm version minor` | Increments minor version. | `npm version minor` |
| `npm version major` | Increments major version. | `npm version major` |

---

### npm doctor
Checks npm environment health.

| Command | Description | Example |
| -------- | ------------ | -------- |
| `npm doctor` | Diagnoses npm setup. | `npm doctor` |

---

### npm exec / npx
Runs binaries from node_modules.

| Command | Description | Example |
| -------- | ------------ | -------- |
| `npx [package]` | Runs package without install. | `npx create-react-app myapp` |
| `npm exec [cmd]` | Runs local binary. | `npm exec eslint .` |

---

## ✅ Tips

- Use `-D` for dev tools (eslint, prettier, vite).
- Prefer `npm ci` in production/CI.
- Always commit `package-lock.json`.
- Run `npm audit` regularly.

---

🚀 Happy Coding!