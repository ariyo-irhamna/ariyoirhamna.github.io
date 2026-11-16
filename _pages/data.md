---
layout: single
title: "Data"
permalink: /data/
author_profile: true
sitemap: false
---

## Permohonan Data PLN

*Data request templates for PT PLN (Persero), January 2010 to September 2026.*

Halaman ini memuat empat template Excel untuk permohonan data penelitian kepada PT PLN (Persero). Kata sandi tercantum dalam surat permohonan.

<div id="pln-gate">
  <form id="pln-form" autocomplete="off">
    <label for="pln-pw">Kata sandi</label><br>
    <input type="password" id="pln-pw" required style="max-width: 18em; width: 100%;">
    <button type="submit" id="pln-btn" class="btn btn--primary">Buka</button>
  </form>
  <p id="pln-msg" role="status" aria-live="polite"></p>
</div>

<div id="pln-content" hidden></div>

Pertanyaan dapat dikirim ke [ariyo.irhamna@indef.or.id](mailto:ariyo.irhamna@indef.or.id).

<script>
(function () {
  var BASE = "{{ '/files/pln/' | relative_url }}";
  var SALT = "IIWal09VF4l1Bk8+wavPeQ==";
  var ITER = 600000;
  var NAMES = {
    "rumah-tangga": "Template Data PLN Rumah Tangga 2010-2026.xlsx",
    "bisnis": "Template Data PLN Bisnis 2010-2026.xlsx",
    "industri": "Template Data PLN Industri 2010-2026.xlsx",
    "desa-jaringan": "Template Data PLN Desa dan Jaringan 2010-2026.xlsx"
  };
  var XLSX = "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet";
  var key = null;
  var msg = document.getElementById("pln-msg");
  var btn = document.getElementById("pln-btn");

  function b64(s) { return Uint8Array.from(atob(s), function (c) { return c.charCodeAt(0); }); }

  function deriveKey(pw) {
    return crypto.subtle.importKey("raw", new TextEncoder().encode(pw), "PBKDF2", false, ["deriveKey"])
      .then(function (base) {
        return crypto.subtle.deriveKey(
          { name: "PBKDF2", salt: b64(SALT), iterations: ITER, hash: "SHA-256" },
          base, { name: "AES-GCM", length: 256 }, false, ["decrypt"]);
      });
  }

  function fetchPlain(slug, k) {
    return fetch(BASE + slug + ".bin", { cache: "no-store" })
      .then(function (r) { if (!r.ok) { throw new Error("fetch"); } return r.arrayBuffer(); })
      .then(function (buf) {
        var b = new Uint8Array(buf);
        return crypto.subtle.decrypt({ name: "AES-GCM", iv: b.slice(0, 12) }, k, b.slice(12));
      });
  }

  function download(e) {
    e.preventDefault();
    var a = e.currentTarget, slug = a.getAttribute("data-enc");
    a.textContent = "Menyiapkan...";
    fetchPlain(slug, key).then(function (plain) {
      var url = URL.createObjectURL(new Blob([plain], { type: XLSX }));
      var t = document.createElement("a");
      t.href = url; t.download = NAMES[slug];
      document.body.appendChild(t); t.click(); t.remove();
      setTimeout(function () { URL.revokeObjectURL(url); }, 10000);
      a.textContent = ".xlsx";
    }).catch(function () { a.textContent = "Gagal, coba lagi"; });
  }

  document.getElementById("pln-form").addEventListener("submit", function (e) {
    e.preventDefault();
    if (!window.crypto || !crypto.subtle) {
      msg.textContent = "Peramban ini tidak mendukung dekripsi. Mohon pakai versi terbaru Chrome, Edge, Firefox, atau Safari.";
      return;
    }
    btn.disabled = true;
    msg.textContent = "Memeriksa kata sandi...";
    var pw = document.getElementById("pln-pw").value;
    var k;
    deriveKey(pw).then(function (dk) { k = dk; return fetchPlain("content", k); })
      .then(function (plain) {
        key = k;
        var box = document.getElementById("pln-content");
        box.innerHTML = new TextDecoder().decode(plain);
        box.querySelectorAll("a[data-enc]").forEach(function (a) { a.addEventListener("click", download); });
        box.hidden = false;
        document.getElementById("pln-gate").hidden = true;
      })
      .catch(function () {
        msg.textContent = "Kata sandi salah atau halaman gagal dimuat. Mohon coba lagi.";
        btn.disabled = false;
      });
  });
})();
</script>
