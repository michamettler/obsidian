#machinelearning #sem5 #labs
### What was your initial question or idea?
Wie war der Verlauf der Hospitalisierungen verglichen mit den Anzahl Toden in Zürich? Ausserdem, wieviel Prozent der Hospitalisierten brauchten über Zeit eine ICU.
### How did you proceed to arrive at an answer?
Zuerst habe ich jeweils die Daten aus dem Datensatz ausgelesen und anschliessend in einem Plot grafisch dargestellt.
### What are your results?
Hospitalisierungen verglichen mit Tode über Zeit:

![[Pasted image 20240920170554.png]]

**Code:**
```python
# extract dates for Geneva
x = covid_data.loc[covid_data['abbreviation_canton_and_fl'] == 'ZH', ['date']]

# extract the 'ncumul_test' column for Geneva
y1 = covid_data.loc[covid_data['abbreviation_canton_and_fl'] == 'ZH', ['current_hosp']]
y2 = covid_data.loc[covid_data['abbreviation_canton_and_fl'] == 'ZH', ['ncumul_deceased']]

# plot
plt.plot_date(x, y1)
plt.plot_date(x, y2)
```

---

Prozentzahl an ICU von Hospitalisierungen über Zeit:

![[Pasted image 20240920171527.png]]

Code:
```python
# extract dates for Geneva
x = covid_data.loc[covid_data['abbreviation_canton_and_fl'] == 'ZH', ['date']]

# extract the 'ncumul_test' column for Geneva
hosp = covid_data.loc[covid_data['abbreviation_canton_and_fl'] == 'ZH', ['current_hosp']]
icu = covid_data.loc[covid_data['abbreviation_canton_and_fl'] == 'ZH', ['current_icu']]
y = (icu['current_icu'] / hosp['current_hosp']) * 100

# plot
plt.plot_date(x, y)
```
