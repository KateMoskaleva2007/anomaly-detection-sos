# Обнаружение аномальных респондентов в активности поисковых запросов SoS

## Автор
**ФИО:** Москалева Екатерина Андреевна
**Группа:** ШЦТ-111

## Описание задачи

Разработать алгоритм для поиска аномально высокой активности отдельных респондентов по отдельным брендам. Аномалия определяется на уровне (SubjectID, researchdate, BrandID, CategoryDelivery). Если респондент признан аномальным хотя бы по одному бренду в день, удаляются все его строки за этот день.

## Алгоритм

**Метод:** Robust Z-Score на основе медианы и MAD (Median Absolute Deviation)

**Формула:** z_score = (daily_ots - median) / MAD

где:
- daily_ots = Weight × количество запросов
- median — медиана daily_ots для бренда
- MAD — медианное абсолютное отклонение

**Порог:** z_score > 8.0

**Почему такой порог?** При пороге 8.0 удаляется 6764 пары респондент-день (2.4%), снижение OTS составляет 30.59%. Более низкие пороги удаляют слишком много данных.

## Запуск

**Установка библиотек:**
pip install -r requirements.txt

**Запуск скрипта:**
python solution_Москалева_ШЦТ-111.py

## Выходные файлы

output/anomalies.csv - список респондентов и дней для удаления
output/anomaly_reasons.csv - причины аномалий
output/plots/total_ots_before_after.png - общий OTS до/после
output/plots/category_ots_change.png - изменение по категориям
output/plots/daily_anomaly_count.png - аномалии по дням
output/plots/gender_comparison.png - сравнение по полу
output/plots/age_comparison.png - сравнение по возрасту
output/plots/resource_comparison.png - сравнение по типу ресурса
output/plots/region_comparison.png - сравнение по округам
output/plots/brand_ots_comparison.png - OTS для бренда apple iphone

## Результаты

Всего строк: 280 458
Валидных строк: 255 748
Найдено аномалий: 8 005
Удаляется пар респондент-день: 6 764
Снижение OTS: 30.59%

**Топ-5 брендов с аномалиями:**
1. apple iphone - 494 аномалий
2. samsung galaxy - 434 аномалий
3. honor - 245 аномалий
4. redmi - 230 аномалий
5. realme - 208 аномалий

## Структура проекта

solution_Москалева_ШЦТ-111.py - основной скрипт
requirements.txt - зависимости
README.md - описание
output/ - папка с результатами