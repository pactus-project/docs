---
title: Pactus Node Configuration
weight: 6
---

The Pactus node can be configured via a TOML file. You can find an example configuration in the
[configurations](https://github.com/pactus-project/pactus/blob/main/config/example_config.toml) section.

Your node configuration can be found at the following path:

{{< tabs items="Linux-mac,windows" >}}
  {{< tab >}}

```
/home/{user}/pactus/config.toml
```

  {{< /tab >}}
  {{< tab >}}

```
C:\Users\{user}\pactus\config.toml
```

  {{< /tab >}}
{{< /tabs >}}

### Example Configuration

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
