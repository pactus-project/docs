---
title: HTTP API Reference
weight: 3
---

<link rel="stylesheet" type="text/css" href="/swagger-ui/swagger-ui.css" />
<link rel="stylesheet" type="text/css" href="/swagger-ui/swagger-ui-dark.css" />
<link rel="stylesheet" type="text/css" href="/swagger-ui/swagger-ui-modify.css" />

<div id="swagger-ui"></div>
<script src="/swagger-ui/swagger-ui-bundle.js" charset="UTF-8"> </script>
<script src="/swagger-ui/swagger-ui-standalone-preset.js" charset="UTF-8"> </script>
<script src="/swagger-ui/swagger-initializer.js" charset="UTF-8"> </script>

<script>
  window.onload = () => {
    window.ui = SwaggerUIBundle({
      url: '/swagger-ui/pactus.swagger.json',
      dom_id: '#swagger-ui',
      presets: [
        SwaggerUIBundle.presets.apis,
        SwaggerUIStandalonePreset
      ],
      layout: "StandaloneLayout",
    });
  };

document.querySelectorAll('#swagger-ui').forEach(function(table) {
  table.classList.add('not-prose');
});

</script>
