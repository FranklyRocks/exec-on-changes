# Execute on Changes GitHub Action

An easy-to-use GitHub Action that detects file changes in the last commit under a specified folder and executes a command if changes are found.

## Features

- Detects changes in the last commit for a specific folder.
- Executes any command if changes are detected.
- Customizable folder path and command via action inputs.
- Ideal for CI/CD pipelines, automation scripts, and more.

## Usage

To use this GitHub Action, create a workflow YAML file (e.g., `.github/workflows/main.yml`) in your repository and include the following content:

```yaml
name: Execute on Changes

on: [push]

jobs:
  check_changes:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Execute on changes
        uses: FranklyRocks/exec-on-changes@v1
        with:
          path: 'your/folder/path'
          command: 'your-command'
```

### Inputs

- `path`: Path where to find changes in files (required).
- `command`: Command to execute if changes in files are found (required).

### Example usages

1. **Restart the queue worker if any queue-related files are changed:**

    ```yaml
    - name: Execute on changes
      uses: FranklyRocks/exec-on-changes@v1
      with:
        path: 'app/Jobs'
        command: 'php artisan queue:restart'
    ```

2. **Run PHPStan for static analysis if any PHP files in the `app` directory are changed:**

    ```yaml
    - name: Execute on changes
      uses: FranklyRocks/exec-on-changes@v1
      with:
        path: 'app'
        command: 'vendor/bin/phpstan analyse'
    ```

3. **Run Laravel Dusk tests if any files in the `tests/Browser` directory are changed:**

    ```yaml
    - name: Execute on changes
      uses: FranklyRocks/exec-on-changes@v1
      with:
        path: 'tests/Browser'
        command: 'php artisan dusk'
    ```

4. **Run style checks if any CSS or SCSS files in the `resources/css` directory are changed:**

    ```yaml
    - name: Execute on changes
      uses: FranklyRocks/exec-on-changes@v1
      with:
        path: 'resources/css'
        command: 'npm run stylelint'
    ```

5. **Run migrations if any migration files are changed:**

    ```yaml
    - name: Execute on changes
      uses: FranklyRocks/exec-on-changes@v1
      with:
        path: 'database/migrations'
        command: 'php artisan migrate'
    ```

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE.md) file for details.

## Support

If you encounter any issues or have any questions, feel free to open an issue on GitHub.