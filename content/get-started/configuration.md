---
title: Pactus Node Configuration
weight: 6
---

## Preface

The Pactus node can configure using a [TOML](https://toml.io/en/) file,
which is a simple text format for configuration.
This file is automatically created when the node initializes.
Each node can have different settings and configurations based on its needs and requirements.

The config file can find inside the working directory, typically located at:

{{< os_tabs items="unix,windows" >}}
  {{< os_tab >}}

```none
~/pactus/config.toml
```

  {{< /os_tab >}}
  {{< os_tab >}}

```none
C:\Users\<USER_NAME>\pactus\config.toml
```

  {{< /os_tab >}}
{{< /os_tabs >}}

## Editing Config File

Modifying the TOML file is straightforward, but because TOML is sensitive to spaces,
it's important to ensure the file is formatted correctly.
Online tools like [TOML Lint](https://www.toml-lint.com/) can help check the validity of the config file.

## Example Configuration

Here is a example of Pactus config file.

<pre><code id="config-code" class="toml">Loading configuration...</code></pre>

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.7.0/styles/atom-one-dark.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.7.0/highlight.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.7.0/languages/toml.min.js"></script>

<script>
  document.addEventListener('DOMContentLoaded', (event) => {
    fetch('https://raw.githubusercontent.com/pactus-project/pactus/main/config/example_config.toml')
      .then(response => {
        if (!response.ok) {
          throw new Error('Network response was not ok');
        }
        return response.text();
      })
      .then(data => {
        const configCode = document.getElementById('config-code');
        configCode.textContent = data;
        hljs.highlightElement(configCode);
      })
      .catch(error => {
        console.error('Error fetching the configuration file:', error);
        const configCode = document.getElementById('config-code');
        configCode.textContent = 'Failed to load configuration file.';
      });
  });
</script>
