# Visualization

## Seaborn

Seaborn is another module for creating diagrams. As with pandas, matplotlib is used in the background, i.e. many settings can be made via matplotlib and used for the actual graphic Seaborn.

```py
import seaborn as sns
m = pd.read_csv("/data/measurements.csv", sep=";",na_values="-")
sns.set(style='darkgrid') # whitegrid
g = sns.catplot(data = m, x = "size", y = "ram", hue="type", palette=["#009bcc","#ff8200","#9bba00"])
g.set(ylim=(0, 10000))
plt.show()

citieslocs = cities.join(locs, rsuffix="Stadtc") sns.relplot(x="Lon" ,y="Lat", data = citieslocs, hue="Landkreis", size="Einwohner",sizes=(200,500))
```
