# TurboWarp scratch-gui Coding Instructions

Important: Always reply in Vietnamese in chat.

This project is a fork of `scratch-gui` modified for TurboWarp. It is a React/Redux application that provides the interface for Scratch 3.0.

## Architecture & Patterns

- **Components vs. Containers**: Follow the strict separation.
    - `src/components/`: Presentational components. Use functional components and CSS Modules.
    - `src/containers/`: Logic and Redux connection. Use Higher-Order Components (HOCs) to wrap components.
- **Higher-Order Components (HOCs)**: Most global logic (VM, storage, project loading) is implemented as HOCs in `src/lib/`.
    - Example: `vm-manager-hoc.jsx` manages the Scratch VM lifecycle.
- **Redux State**: State is managed in `src/reducers/`. The root reducer is in `src/reducers/gui.js`.
    - Access state via `mapStateToProps` in containers.
    - Dispatch actions via `mapDispatchToProps`.
- **Scratch VM Integration**: The `scratch-vm` instance is central. It's typically passed as a `vm` prop. Use `vm-listener-hoc.jsx` to react to VM events.
- **Core Libraries**:
    - `scratch-vm`: The execution engine.
    - `scratch-storage`: Handles loading and saving of projects and assets.
    - `scratch-blocks`: The block-based editor (based on Blockly).
    - `scratch-render`: The WebGL renderer for the stage.
- **Addons System**: Located in `src/addons/`. This integrates Scratch Addons.
    - `src/addons/api.js` provides the API for addons.
    - `src/addons/hooks.js` contains hooks called by the GUI to trigger addon logic.
- **TurboWarp Specifics**: Features unique to TurboWarp are often prefixed with `tw-` (e.g., `src/components/tw-project-input/`).

## Development Workflow

- **Start Development**: `npm start` (runs on [http://localhost:8601/](http://localhost:8601/)).
- **Build**: `npm run build` (outputs to `build/` and `dist/`).
- **Testing**:
    - `npm run test:lint`: Linting with ESLint.
    - `npm run test:unit`: Unit tests (mostly for addons).
    - `npm run test:integration`: Integration tests using Jest.
- **Internationalization**: Use `react-intl`.
    - Define messages using `defineMessages` from `react-intl`.
    - Use `FormattedMessage` or `intl.formatMessage` for display.
    - Translations are managed via `@turbowarp/scratch-l10n`.

## Coding Standards

- **Styling**: Use CSS Modules. Import styles as `import styles from './filename.css'` and apply using `styles.className`.
- **Utilities**: Prefer `lodash` utilities (e.g., `bindAll`, `debounce`, `throttle`) which are already dependencies.
- **Prop Types**: Always define `propTypes` for components to ensure type safety.
- **File Naming**: Use kebab-case for directories and files, except for React components/containers which use kebab-case for directories and PascalCase or kebab-case for files (follow existing patterns in the specific directory).

## Key Files to Reference

- `src/lib/app-state-hoc.jsx`: Entry point for Redux store initialization.
- `src/reducers/gui.js`: Main GUI state definition.
- `src/containers/gui.jsx`: The main GUI container.
- `src/components/gui/gui.jsx`: The main GUI presentational component.
- `src/addons/hooks.js`: Integration point for the addons system.
