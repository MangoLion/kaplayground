# Kaplayground Project Structure Report

This report provides a detailed overview of the Kaplayground web editor's file structure, with a special focus on UI-related components and main code files. The analysis is based on the project's file and directory names.

## 1. Overall Project Structure

The project is a modern web application, likely built with React and TypeScript, given the `.tsx` file extensions and `tsconfig.json`. Key top-level directories and files include:

-   **`public/`**: Contains static assets served directly by the web server (e.g., `index.html` for a sandbox, `pg.png`).
-   **`sandbox/`**: Appears to be a dedicated environment for running/testing Kaplay games, possibly in an iframe. It has its own `index.html` and `vite.config.ts`.
-   **`scripts/`**: Contains utility scripts, possibly for development or build processes (e.g., `examples.ts`, `types.ts`).
-   **`src/`**: The main source code directory for the Kaplayground application.
    -   **`components/`**: Houses the reusable UI components that make up the editor's interface. This is a key area for UI analysis.
    -   **`config/`**: Application configuration files (e.g., `common.ts`, `defaultProject.ts`).
    -   **`data/`**: Static data used by the application (e.g., `demos.ts`, `exampleList.json`).
    -   **`features/`**: Contains modules for specific application features, likely encapsulating business logic and potentially UI elements related to those features.
    -   **`hooks/`**: Custom React hooks for reusable stateful logic.
    -   **`styles/`**: Global styles and CSS files.
    -   **`util/`**: Utility functions and helper modules.
    -   **`App.tsx`**: The root React component of the application.
    -   **`main.tsx`**: The main entry point of the application, likely where the React app is initialized and mounted to the DOM.
-   **Configuration Files**:
    -   `package.json`: Project metadata, dependencies, and scripts.
    -   `vite.config.ts`: Configuration for the Vite build tool.
    -   `tailwind.config.js`: Configuration for Tailwind CSS.
    -   `tsconfig.json` (and variants): TypeScript compiler options.

## 2. Main Application Entry Points

-   **`src/main.tsx`**: This is the primary entry point where the React application is bootstrapped. It likely imports `App.tsx` and renders it into the HTML.
-   **`src/App.tsx`**: The root component of the application. It sets up the main layout, routing (if any), and integrates various top-level components and features.

## 3. UI Components (`src/components/`)

This directory is central to the application's user interface. Components are organized by their functionality:

### 3.1. Core UI Elements (`src/components/UI/`)

This subdirectory seems to contain generic, reusable UI building blocks:
-   **`Dialog.tsx`**: A base component for creating modal dialogs.
-   **`TabsList.tsx` / `TabTrigger.tsx`**: Components for implementing tabbed interfaces.
-   **`View.tsx`**: Potentially a generic container or layout component.
-   **`KDropdown/`**: Custom dropdown components.
    -   `KDropdownSeparator.tsx`

### 3.2. Editor Components (`src/components/Editor/`)

Components related to the code editing experience:
-   **`MonacoEditor.tsx`**: The core code editor component, likely integrating the Monaco Editor (the engine behind VS Code).
-   **`completionProviders.ts`**: Logic for custom code completion.
-   **`monacoConfig.ts`**: Configuration specific to the Monaco Editor instance.
-   **`actions/`**: Editor-specific actions (e.g., `format.ts`).
-   **`completion/`**: Autocompletion logic, including `KAPLAYSnippets.ts`.
-   **`snippets/`**: Code snippets, such as `compSnippets.ts`.
-   **`themes/`**: Editor themes (e.g., `themes.ts`).

### 3.3. File System Navigation (`src/components/FileTree/`)

Components for displaying and interacting with the project's file structure:
-   **`FileTree.tsx`**: The main component for the file tree sidebar.
-   **`FileEntry.tsx`**: Represents a single file in the tree.
-   **`FileFold.tsx` / `FileFolder.css`**: Represents a folder in the tree. (Note: `FileFold.tsx` might be a typo and intended to be `FileFolder.tsx` or similar, or it handles the folding mechanism).
-   **`FileToolbar.tsx`**: Toolbar associated with the file tree (e.g., for creating files/folders).

### 3.4. Toolbar and Controls (`src/components/Toolbar/`)

Components that form the main application toolbar:
-   **`Toolbar.tsx`**: The main toolbar container.
-   **`ToolbarButton.tsx`**: A generic button for the toolbar.
-   **`ToolbarDropdown.tsx` / `ToolbarDropdownButton.tsx`**: Dropdown menus for the toolbar.
-   **`ExampleList.tsx`**: Likely a dropdown or list for selecting example projects.
-   **`ProjectStatus.tsx`**: Displays the status of the current project.
-   **`ToolbarProjectDropdown.tsx`**: Specific dropdown for project-related actions.
-   **`ToolbarToolsMenu.tsx`**: Menu for various tools.
-   **`ToolButtons/`**: Specific action buttons for the toolbar:
    -   `AboutButton.tsx`
    -   `ConfigButton.tsx`
    -   `ShareButton.tsx`

### 3.5. Asset Management (`src/components/Assets/` & `src/components/AssetBrew/`)

Components related to managing project assets:
-   **`src/components/Assets/`**:
    -   **`AssetsPanel.tsx`**: The main panel for displaying and managing assets.
    -   **`Assets.tsx`**: Core logic or container for asset display.
    -   **`AssetsAddButton.tsx`**: Button for adding new assets.
    -   **`AssetsItem.tsx` / `AssetsList.tsx`**: Components for displaying individual assets and lists of assets.
    -   **`AssetsTab.tsx`**: Tab for accessing the assets panel.
-   **`src/components/AssetBrew/`**:
    -   **`AssetBrew.tsx`**: UI for the "Asset Brew" feature (importing default assets).
    -   **`AssetBrewItem.tsx`**: Represents an item within the Asset Brew interface.

### 3.6. Project Management (`src/components/ProjectBrowser/`)

Components for opening, creating, and managing projects:
-   **`ProjectBrowser.tsx`**: The main UI for browsing local projects.
-   **`ProjectCreate.tsx`**: UI for creating new projects.
-   **`ProjectEntry.tsx`**: Represents a single project in the browser list.
-   **`GroupBy.tsx` / `SortBy.tsx` / `TagsFilter.tsx`**: UI elements for filtering and organizing projects.

### 3.7. Game View / Playground (`src/components/Playground/`)

Components responsible for running and displaying the Kaplay game:
-   **`Playground.tsx`**: The main container for the game execution environment.
-   **`GameView.tsx`**: The specific component that renders the game, likely an iframe or canvas.
-   **`LoadingPlayground.tsx`**: UI shown while the playground is loading.
-   **`WorkspaceExample.tsx` / `WorkspaceProject.tsx`**: Components possibly differentiating between running an example and a full project.

### 3.8. Other UI Components

-   **`src/components/About/AboutDialog.tsx`**: Dialog displaying information about Kaplayground.
-   **`src/components/Config/ConfigDialog.tsx`**: Dialog for application or project configuration.
    -   `ConfigEditor.tsx`
    -   `ConfigForm/`: Contains form elements like `ConfigCheckbox.tsx`, `ConfigSelect.tsx`.
-   **`src/components/ConsoleView/ConsoleView.tsx`**: UI for displaying console logs from the game or editor.

## 4. Feature Modules (`src/features/`)

This directory organizes code by specific application features. While primarily for logic, these can also include or be closely tied to UI components.

-   **`src/features/Editor/`**:
    -   **`application/insertAfterCursor.ts`**: Logic for editor actions.
-   **`src/features/Projects/`**: This is a significant feature module.
    -   **`application/`**: Contains business logic for project handling:
        -   `buildCode.ts`
        -   `buildProject.ts`
        -   `wrapCode.ts`
        -   `wrapGame.ts`
    -   **`models/`**: Defines data structures (models) for the project feature:
        -   `Asset.ts`, `AssetKind.ts`
        -   `File.ts`, `FileFolder.ts`, `FileKind.ts`
        -   `Project.ts`, `ProjectMode.ts`
        -   `UploadAsset.ts`
    -   **`stores/`**: State management for projects, likely using a library like Zustand or Redux Toolkit:
        -   `useProject.ts` (custom hook for accessing project state)
        -   `slices/`: Defines different parts of the project state (`assets.ts`, `files.ts`, `project.ts`).

## 5. Styling (`src/styles/`)

-   **`index.css`**: Main stylesheet, possibly importing others or defining global styles.
-   **`toast.css`**: Styles for notification/toast messages.
-   **Tailwind CSS**: Indicated by `tailwind.config.js` and `postcss.config.js`, suggesting utility-first CSS is heavily used throughout the components. Individual components might also have their own CSS files (e.g., `AssetsPanel.css`, `FileEntry.css`).

## 6. Hooks (`src/hooks/`)

Custom React hooks provide reusable stateful logic and side effects, often used by UI components:
-   **`useAssets.ts`**: Hook for managing or accessing asset-related data.
-   **`useConfig.ts`**: Hook for managing or accessing configuration.
-   **`useEditor.ts`**: Hook for interacting with the editor state or functionalities.

## 7. Utilities (`src/util/`)

General utility functions that can be used across the application, including by UI components for data transformation, event handling, etc. Examples:
-   `cn.ts`: Likely a utility for conditionally joining class names (common with Tailwind CSS).
-   `compressCode.ts`: Utility for code compression.
-   `download.ts`: For file downloads.
-   `fileToBase64.ts`: For converting files to Base64.
-   `logs.ts`: For handling or formatting logs.

## Summary of UI Focus

The UI of Kaplayground is primarily constructed using React components located in `src/components/`. These components are well-organized by their domain (Editor, FileTree, Toolbar, Assets, etc.). Generic UI primitives are found in `src/components/UI/`. State management related to features like "Projects" (which heavily influences the UI) is handled in `src/features/Projects/stores/`, and custom hooks in `src/hooks/` further support UI logic. Styling is a mix of global CSS, component-specific CSS, and Tailwind CSS.

The application appears to follow a component-based architecture, promoting reusability and separation of concerns, which is typical for modern web applications built with frameworks like React.
