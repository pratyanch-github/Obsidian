When I mentioned the **installed version of React**, I was referring to the version of React listed in your **project's dependencies** (typically specified in the `package.json` file of your project). This is a **local installation** of React that is installed specifically for the project when you run `npm install`.

Here’s how it works:

---

### **1. Local Installation (Per Project)**

- When you install React for a project (e.g., `npm install react`), it is added to the `node_modules` directory within your project.
- The version of React specified in the `dependencies` or `devDependencies` section of your `package.json` file is what determines the "installed version" for that project.
- This local version is what your project uses during development or production.

---

### **2. Global Installation**

- You might install packages like `npm install -g <package>` globally for tools like `create-react-app`, `eslint`, or others that you want to use system-wide.
- React itself is **not usually installed globally**, as each project typically uses its own version to avoid version conflicts.

---

### **Checking the Installed Version of React**

- To see the React version used in your project:
    
    ```bash
    npm list react
    ```
    
    or
    
    ```bash
    yarn list react
    ```
    
- To check the version of React globally installed (if any):
    
    ```bash
    npm list -g react
    ```
    

---

### **Why Does This Matter?**

The error you're encountering is about a **peer dependency conflict**. This happens because:

1. Your project is using `react@18.2.0`.
2. The `@mdx-js/react` package has a `peerDependency` requirement of `react@"^16.13.1 || ^17.0.0"`, meaning it only officially supports React 16 or 17.

This conflict is resolved by:

- Adjusting your **local React version** in the project.
- Upgrading the `@mdx-js/react` package (if it supports React 18).
- Using flags like `--legacy-peer-deps` or `--force` to bypass strict dependency resolution.

Let me know if you'd like more clarification or help with fixing the issue!