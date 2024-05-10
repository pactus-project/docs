---
title: HTTP API Reference
weight: 2
---

<link rel="stylesheet" href="/swagger-ui/swagger-ui.css" />
<link rel="stylesheet" href="/swagger-ui/swagger-ui-dark.css" />
<link rel="stylesheet" href="/swagger-ui/swagger-ui-modify.css" />
<div id="swagger-ui"></div>
<script src="/swagger-ui/swagger-ui-bundle.js" crossorigin></script>
<script src="/swagger-ui/swagger-ui-standalone-preset.js" crossorigin></script>
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
</script>
<script>
document.addEventListener('DOMContentLoaded', function() {
  if (localStorage.getItem('color-theme') === "dark") {
    document.documentElement.setAttribute('data-bs-theme', 'dark')
  }
})
</script>