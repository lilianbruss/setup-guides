# Introducing Automation with Dynaconf

In order to make source code more independent from manual parameter adjustments, we use Dynaconf to avoid hard-coded information.
The application offers complex configuration management for Python, including features such as settings management (defaults vs special cases), handling of 
sensitive information, environment variables, and multiple environments.

---

## Installation and Default Configuration Files

To get started, add Dynaconf to your Python environment. For example, if you're using `uv`, run:

- `uv add dynaconf`


After setting up Dynaconf, your project will typically include the following configuration files:

- `settings.toml`: This is the main configuration file in your root directory. It can contain multiple environment sections like [default], [development], [test], etc. Example:

  ```
  [default] # used when no specific environment is set
  debug = true

  [test] # used under specific testing conditions
  debug = false
  ```

- `.secrets.toml`: This file is used to store sensitive data such as API keys or passwords and is usually excluded for mversion control.

- `.env`: A simple environment file where you can define shell environment variables, including ENV_FOR_DYNACONF and any prefixed variables like DYNACONF_DB_URL.

Additionally, a `config.py` file is used to load these settings dynamically.

```
from dynaconf import Dynaconf


settings = Dynaconf(
    auto_cast = True, # enable explicit type-casting of variables
    envvar_prefix="DYNACONF", # prefix of Dynaconf environment variables
    environments=True, # enable multiple environments
    default_env="default", # set default environment to fall back to
    env=venv_name, # set active environment during run-time
    settings_files=['settings.toml', '.secrets.toml'] # load setting files in that order 
)
```
In case the virtual environment is activated in the shell, the configuration file `config.py` can be modified to refer to the respective Dynaconf environment in `settings.toml` automatically by setting the parameter `env=venv_name` to synchronize with the active virtual environment during run-time.

Dynaconf automatically loads these files (unless configured otherwise), and applies settings based on the defined precedence.

### Precedence order (from highest to lowest):

#### In-memory assignment
- Example in Python script: `setting.var=value`
- Temporary and does not persist to TOML or shell.

#### Environment variables
- Set via shell (`export DYNACONF_VAR=value`) or .env file ( `echo $DYNACONF_VAR=value`).
- Good for sensitive or deployment-specific data.
- Dynaconf uses the prefix DYNACONF_ by default.

#### TOML configuration (settings.toml)
- Persistent, version-controlled settings under [default], [test], etc.

#### Dynaconf defaults
- Passed explicitly to the Dynaconf instance in `config.py`.

Since environment variables or even run-time assignment of a setting variable take priority over the baseline configurations, simply type `export ENV_FOR_DYNACONF=env_name` in your shell to switch to the specified section `env_name` in `settings.toml`.


## References & Further Reading:
- [Dynaconf Quick Start](https://www.dynaconf.com/)
- [Project Description of an Older Version](https://pypi.org/project/dynaconf/0.7.6/)