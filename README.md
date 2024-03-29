# Эмулятор лифта

## Установка
```
cd lift-emulator
npm install
npm run start
```
## Вид приложения
![image](https://github.com/flamaster00/lift-emulator/assets/55953131/7381bbd8-f042-4b9b-900f-3b4f497c72e1)

## Описание ТЗ
Требуется разработать одностраничное приложение (SPA), эмулирующее работу лифтовой системы.
Приложение должно состоять из схемы нескольких этажей с нумерацией и кнопками вызова, а также из самой шахты лифта с кабиной.
- Количество этажей по умолчанию: 5.
- Количество шахт лифта по умолчанию: 1.
- По умолчанию лифт находится на 1 этаже в состоянии покоя (свободен).

При нажатии на кнопку вызова лифт должен обработать этот вызов в
соответствии со следующими сценариями:

1. Если вызов осуществляется с этажа, на котором лифта нет –
свободный лифт начинает движение к выбранному этажу со
скоростью 1 этаж в секунду.
Достигнув нужного этажа лифт 3 секунды «отдыхает» -
индикацию этого состояния можно реализовать с помощью
мигания.
После этого лифт снова переходит в состояние покоя и готов
обработать следующий вызов.

2. Если в момент движения лифта осуществить вызов на другой
этаж – этот вызов должен добавиться в очередь вызовов.
Вызовы должны обрабатываться последовательно.

3. Вызов пропускается в случаях, если:
- лифт уже находится на выбранном этаже в состоянии покоя
- лифт уже находится в процессе обработки такого вызова
(находится в движении к выбранному этажу)
- в очереди вызовов уже есть выбранный этаж

