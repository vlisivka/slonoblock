---
layout: post
title: Розрахунок термоакумулятора
author: Володимир Лісівка
comments: true
usemathjax: true
---
<script>
  function p(str) { document.write(str); }

  // Print number in locale specific way.
  var locale_format = new Intl.NumberFormat('uk-UA');
  function pn(number) { document.write(locale_format.format(number)); }
  function pbn(number) { document.write('<b>',locale_format.format(number),'</b>'); }
  
  
</script>

# Розрахунок термоакумулятора для будинку 10x8x5м

## Кількість градусоднів опалення

Градусдень (гд) — це кількість днів, коли потрібне опалення, помножене на кількість градусів, на яку треба підігрівати будинок порівняно із зовнішнім середовищем.

Напр., якщо на вулиці температура +10°Ц, а у будинку +20°Ц, то це $(20-10) \cdot 1 = 10$ гд.

