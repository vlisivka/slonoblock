---
layout: post
title: Розрахунок тепловтрат будівлі
author: Володимир Лісівка
comments: true
usemathjax: true
---

<script>
  window.PlotlyConfig = {MathJaxConfig: 'local'}

  function p(str) { document.write(str); }

  // Print number in locale specific way.
  var locale_format = new Intl.NumberFormat('uk-UA');
  function pn(number) { document.write(locale_format.format(number)); }
  function pbn(number) { document.write('<b>',locale_format.format(number),'</b>'); }

  var температура_ззовні = -20; // °C
  var температура_в_будинку = 20; // °C
  var різниця_температур = температура_в_будинку - температура_ззовні; // K

  var довжина_будинку = 10, ширина_будинку = 8, висота_будинку = 2*2.5; // m
  var товщина_стіни = 0.4; // m
  var теплопровідність_соломи = 0.06; // Wt/m*K

  var назва_вікна = 'KBE 88 Passiv';
  var теплопровідність_вікон = 0.81; // Wt/m²*K
  var ширина_вікна = 1.32, висота_вікна = 1.42; // m
  var кількість_вікон = 11;

  var назва_дверей = 'Вхідні утеплені пінопластом 40мм';
  var теплопровідність_дверей = 1.5; // Wt/m²*K
  var ширина_двері = 1.2, висота_двері = 2.1; // m
  var кількість_дверей = 2;
</script>

# Розрахунок термічних властивостей будівлі при -20°Ц

Тепловтрати двоповерхового будинку з Слоноблоків розміром <script>pn(довжина_будинку)</script>x<script>pn(ширина_будинку)</script> м.

## Формула для обрахунку втрат тепла

Втрати тепла через поверхні  вимірюються як:

$$ Q = S \cdot U \cdot ΔT$$

де

  * $S$ — це площа поверхні (м²),
  * $U$ — теплопровідність поверхні (усереднена, Вт/м²°Ц),
  * $ΔT$ — різниця температур (при комфортній температурі в <script>pn(температура_в_будинку)</script>°Ц у будинку, і при температурі <script>pn(температура_ззовні)</script>°Ц ззовні, різниця температур складає <script>pn(різниця_температур)</script>°Ц).

## Втрати тепла через вікна

<script>
try {
  var площа_вікна = ширина_вікна * висота_вікна; // m²
  var площа_вікон = площа_вікна * кількість_вікон; // m²
  var втрати_тепла_через_вікна = теплопровідність_вікон * площа_вікон * різниця_температур; // Wt

} catch(e) { document.write(e); }
</script>

Втрати тепла через вікна розраховуються по тій самій формулі.

Площа $S_w$ для <script>pn(кількість_вікон)</script> вікон розміром <script>pn(ширина_вікна)</script>x<script>pn(висота_вікна)</script> м складає <script>pbn(площа_вікон)</script> м².

Теплопровідність вікон $Uw$ для вікон «<script>p(назва_вікна)</script>» складає <script>pbn(теплопровідність_вікон)</script> Вт/м²°Ц.

Втрати тепла $Qw$ через вікна складатимуть <script>pbn(втрати_тепла_через_вікна);</script> Вт.

## Втрати тепла через двері

<script>
try {
  var площа_двері = ширина_двері * висота_двері; // m²
  var площа_дверей = площа_двері * кількість_дверей; // m²
  var втрати_тепла_через_двері = теплопровідність_дверей * площа_дверей * різниця_температур; // Wt

} catch(e) { document.write(e); }
</script>

Втрати тепла через дверей розраховуються по тій самій формулі.

Площа $S_d$ для <script>pn(кількість_дверей)</script> дверей розміром <script>pn(ширина_двері)</script>x<script>pn(висота_двері)</script> м складає <script>pbn(площа_дверей)</script> м².

Теплопровідність дверей $U_d$ для дверей «<script>p(назва_дверей)</script>» складає <script>pbn(теплопровідність_дверей)</script> Вт/м²°Ц.

Втрати тепла $Q_d$ через двері складатимуть <script>pbn(втрати_тепла_через_двері);</script> Вт.

## Втрати тепла через стіни

<script>
try {
  var теплопровідність_стіни = теплопровідність_соломи / товщина_стіни; // Wt/m²*K
  var площа_стін = 2*(довжина_будинку + ширина_будинку) * висота_будинку; // m²
  var площа_стелі = довжина_будинку * ширина_будинку; // m²
  var площа_поверхні_будинку = площа_стін + площа_стелі - площа_вікон - площа_дверей; // m²
  var втрати_тепла_через_стіни = теплопровідність_стіни * площа_поверхні_будинку * різниця_температур; // Wt

} catch(e) { document.write(e); }
</script>

Втрати тепла через стіни та стелю розраховуються як

$$ Q_b = S_b \cdot ΔT \cdot λ / d$$

де 

  * $d$ — товщина утеплювача стін та стелі(м),
  * $λ$ — коефіцієнт теплопровідності стіни з утеплювачем (усереднений, Вт/м°Ц).

Усереднена теплопровідність стін $U_d = λ / d$ з утеплювачем товщиною <script>pn(товщина_стіни)</script> м з соломи, при коефіцієнті теплопровідності соломи $λ$ у <script>pn(теплопровідність_соломи)</script> Вт/м°Ц, складає <script>pbn(теплопровідність_стіни)</script> Вт/м²°Ц.

Загальна площа $S = 2 \cdot l \cdot h + 2 \cdot w \cdot h + l \cdot w$ утеплених зовнішніх поверхонь будинку розміром <script>pn(довжина_будинку)</script>x<script>pn(ширина_будинку)</script>x<script>pn(висота_будинку)</script> м, без врахування площі фундаменту та вікон і дверей: <script>pbn(площа_поверхні_будинку)</script> м².

Таким чином, втрати тепла через стіни $Q_b$ складатимуть <script>pbn(втрати_тепла_через_стіни)</script> Вт.


## Втрати тепла через вентиляцію

<script>
try {
  var кількість_змін_повітря_на_день = 3;
  var ккд_рекуператора = 0.5; // При -20°Ц
  var густина_повітря = 1.29; // kg/m³
  var теплоємність_повітря = 1000; // J/kg*K

  var обʼєм_будинку = довжина_будинку * ширина_будинку * висота_будинку; // m³

  var обʼєм_повітря_на_день = обʼєм_будинку * кількість_змін_повітря_на_день; // m³/day
  var обʼєм_повітря_на_секунду = обʼєм_повітря_на_день/(24*60*60); // m³/s
  var різниця_температур_для_догрівання = різниця_температур * ккд_рекуператора; // K
  var втрати_тепла_через_вентиляцію = обʼєм_повітря_на_секунду * густина_повітря * теплоємність_повітря * різниця_температур_для_догрівання; // J/s або Wt

} catch(e) { document.write(e); }
</script>

Втрати тепла через вентиляцію з рекуператором тепла рахуються як

$$ Q_v = v \cdot ρ \cdot c \cdot ΔT_v$$

де

  * $v$ — обʼєм повітря, який вентилюється за секунду (м³/с),
  * $ρ$ — густина повітря (<script>pn(густина_повітря)</script> кг/м³),
  * $с$ - коефіцієнт теплоємності повітря (<script>pn(теплоємність_повітря)</script> Дж/кг°Ц),
  * $ΔT_v$ — різниця температур, на яку потрібно підігріти повітря після проходження через рекуператор.

Обʼєм повітря, який вентилюється, розраховується як

$$v = V \cdot n / D $$

де

  * $V$ — це обʼєм повітря у будинку (м³),
  * $n$ — кількість змін повітря за добу (раз),
  * $D$ — кількість секунд у добі (86400 с).

Для комфорту, при поточних значеннях рівня CO2 у повітрі, рекомендується змінювати повітря <script>pn(кількість_змін_повітря_на_день)</script> рази на добу. Таким чином, обʼєм будинку $V$ складає <script>pn(обʼєм_будинку)</script> м³, а швидкість вентилювання $v$ — <script>pbn(обʼєм_повітря_на_секунду)</script> м³/с.

Ефективність рекуператора при <script>pn(температура_ззовні)</script>°Ц складає <script>pn(ккд_рекуператора*100)</script> %. Тобто, після проходження рекуператора, температура зовнішнього повітря піднімається до <script>pn(температура_ззовні+різниця_температур * ккд_рекуператора)</script>°Ц, а отже потрібно догріти <script>pn(обʼєм_повітря_на_секунду)</script> м³ повітря на <script>pn(різниця_температур_для_догрівання)</script>°Ц.

Відповідно $Q_v$ складає <script>pbn(втрати_тепла_через_вентиляцію)</script> Вт (або Дж/с).

---

## Сумарні втрати тепла
<script>
try {
  var сумарні_втрати_тепла = втрати_тепла_через_стіни + втрати_тепла_через_вікна + втрати_тепла_через_двері + втрати_тепла_через_вентиляцію; // Wt
} catch(e) { document.write(e); }
</script>


Сумарні втрати тепла будинку через стіни, стелю, вікна, двері, та вентиляцію можна порахувати як

$$ Q = Q_b + Q_w + Q_d + Q_v$$

і вони складають <script>pbn(сумарні_втрати_тепла)</script> Вт.

## Розподіл втрат тепла за категоріями

<script src='https://cdn.plot.ly/plotly-basic-latest.min.js'></script>
<div id='heat_loss_contibution_chart'><!-- Plotly chart will be drawn inside this DIV --></div>
<script>
var heat_loss_contibution_chart_data = [{
  values: [втрати_тепла_через_стіни, втрати_тепла_через_вікна, втрати_тепла_через_двері, втрати_тепла_через_вентиляцію],
  labels: ['Стіни', 'Вікна', 'Двері', 'Вентиляція'],
  type: 'pie'
}];

Plotly.newPlot('heat_loss_contibution_chart', heat_loss_contibution_chart_data);
</script>

## Потужність системи опалення

<script>
try {
  var надлишковість_системи_опалення = 3;
  var дисконт_температури_жилого_будинку = 4.5; // K
  var потужність_системи_опалення = надлишковість_системи_опалення * сумарні_втрати_тепла * (різниця_температур - дисконт_температури_жилого_будинку)/різниця_температур; // Wt
} catch(e) { document.write(e); }
</script>

Опалювальна система для будинку вибирається із запасом 3х, щоб мати можливість швидко розігріти будинок при потребі. З іншого боку, при проживанні у будинку, люди та побутові прилади споживають енергію та виділяють тепло, а у не жилому будинку вентиляція не потрібна і температура може бути нижчою. Також, сонце гріє будинок через вікна. Традиційно, з врахуванням додаткових джерел тепла, внутрішня температура будинку розраховується з дисконтом $δ$ 4,5°Ц, тобто +15,5°Ц. Тоді потужність системи опалення повинна бути не меншою ніж $P = 3 \cdot Q \cdot (ΔT - δ) / ΔT$, що складає <script>pbn(потужність_системи_опалення)</script> Вт.
