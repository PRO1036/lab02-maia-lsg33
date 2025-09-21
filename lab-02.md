Lab 02 - Plastic waste
================
LE SCOUARNEC Maïa
21/09/2025

## Chargement des packages et des données

``` r
library(tidyverse) 
```

``` r
plastic_waste <- read_csv("data/plastic-waste.csv")
```

Commençons par filtrer les données pour retirer le point représenté par
Trinité et Tobago (TTO) qui est un outlier.

``` r
plastic_waste <- plastic_waste %>%
  filter(plastic_waste_per_cap < 3.5)
  ggplot(data = plastic_waste, 
         aes(x = plastic_waste_per_cap, fill = continent)) +
  geom_histogram(binwidth = 0.2, alpha = 0.85, color="grey")+
    labs(x= "quantité de plastique non gérés", y = "continent")
```

![](lab-02_files/figure-gfm/filter-data-1.png)<!-- -->

## Exercices

### Exercise 1

``` r
ggplot(data = plastic_waste,
       aes(x= plastic_waste_per_cap, fill = continent))+
  geom_histogram(binwidth = 0.2, alpha = 0.75, color = "grey")+
  labs(x= "quantité de plastique non gérés", y = "continent" )+
  labs(y="Continent", x= "Déchets plastiques par habitant", title="Quantité de déchet plastiques par habitant en fonction des continents")+
  facet_wrap(~continent)
```

![](lab-02_files/figure-gfm/plastic-waste-continent-1.png)<!-- --> On
remarque que le continent Américian ( Nord et Sud) et le continent
asiatique ont des pays qui produisent plus de 0.5 tonne de plastique
contrairement aux autres continents qui voit leur production inférieure
à 0.5. ON voit aussi que la majorité des pays de chaque continent ont
quand même une production de plastique inférieur à 0.25 tonnes.

### Exercise 2

``` r
ggplot(data = plastic_waste,
       aes(x= plastic_waste_per_cap, color = continent, fill = continent))+
  geom_density(size= 0.15,alpha= 0.5)+
  labs(y="Densité", x= "Déchets plastiques paar habitant", title="Densité de déchet plastique par habitant", subtitle = "Selon le continent")
```

    ## Warning: Using `size` aesthetic for lines was deprecated in ggplot2 3.4.0.
    ## ℹ Please use `linewidth` instead.
    ## This warning is displayed once every 8 hours.
    ## Call `lifecycle::last_lifecycle_warnings()` to see where this warning was
    ## generated.

![](lab-02_files/figure-gfm/plastic-waste-density-1.png)<!-- -->

Color, fill se trouvent dans aes car ils sont conditionnés pour chaque
variable, alors que alpha se trouve dans geom_density car on souhaite
que toutes les variables soient à la même transparence.

### Exercise 3

Boxplot:

``` r
ggplot(data = plastic_waste,
       aes(x= continent, y= plastic_waste_per_cap, color = continent))+
  geom_boxplot()+
  labs(y="Nombre de déchets plastiques par habitant", x= "Continent", title="Quantité de déchet plastiques par habitant en fonction des continents")
```

![](lab-02_files/figure-gfm/plastic-waste-boxplot-1.png)<!-- -->

Violin plot:

``` r
ggplot(data = plastic_waste,
       aes(x= continent, y= plastic_waste_per_cap, fill = continent))+
  geom_violin()+
  labs(y="Nombre de déchets plastiques par habitant", x= "Continent", title="Quantité de déchet plastiques par habitant en fonction des continents")
```

![](lab-02_files/figure-gfm/plastic-waste-violin-1.png)<!-- -->

Le graphe violin permet de mieux voir la répartiton dans les continents,
il possède une meilleure précision de l’uniformité ou non de la
production de plastique en tonne. Par exemple sur le graph box on ne
voit pas de médiane dans la moyenne de l’Amérique du Nord, or grace au
violin on voit bien que l’on à une majorité entre 0.25 et 0.3 tonnes de
porduction de plastique.

De plus on comprend mieux les points qui apparaissaient sur le graph
box.

### Exercise 4

``` r
ggplot (data= plastic_waste, 
        aes (x= plastic_waste_per_cap, y=mismanaged_plastic_waste_per_cap, color= continent))+
  geom_point()+
  labs(y="Nombre de déchets plastiques non gérés par habitant", x= "Nombre de déchets plastiques par habitant ", title="Quantité de déchet plastiques non gérés en fonction de la quantité de déchets plastique par habitant", subtitle="Selon le continent" )
```

![](lab-02_files/figure-gfm/plastic-waste-mismanaged-1.png)<!-- -->

Le nuage de point montre qu’il existe une relation entre la production
de déchet et la quantité qui est mal gérée. On remarque que plus le
continent produit de déchet par habitant, moins il est en capacité de
les gérer correctement. Pourtant on remarque quelques points qui ne
suivent pas la tendance. Cela montre que certains pays malgrés une
production faible de déchet ne sont pas en capacité de les gérer. (Ex le
point marron représentant un pays d’Asie)

### Exercise 5

``` r
ggplot (data= plastic_waste, 
        aes (x= plastic_waste_per_cap, y=total_pop, color= continent))+
  geom_point()+
  labs(y="Population total", x= "Nombre de déchets plastiques par habitant ", title="Quantité de déchet plastiques en fonction population ", subtitle="Selon le continent" )
```

    ## Warning: Removed 10 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](lab-02_files/figure-gfm/plastic-waste-population-total-1.png)<!-- -->

``` r
ggplot (data= plastic_waste, 
        aes (x= plastic_waste_per_cap, y=coastal_pop, color= continent))+
  geom_point()+
  labs(y="Population côtière", x= "Nombre de déchets plastiques par habitant ", title="Quantité de déchet plastiques en fonction population côtière", subtitle="Selon le continent" )
```

![](lab-02_files/figure-gfm/plastic-waste-population-coastal-1.png)<!-- -->

On remarque qu’il est compliqué de lire le graph 1 car la population est
tres grand et cela rend compliqué l’observation entre le nombre total
d’habitant et la porduction de déchet par habitant. Par contre pour le
graph 2, on remarque que les contients avec une plus grande population
cotière ont une production de déchets plus élevée par habitant. Par
exemple l’Océanie qui est très cotière, à une plus grande production de
déchet par habitant, que l’Asie qui a beaucoup moins de territoires
cotiers.

## Conclusion

Recréez la visualisation:

``` r
plastic_waste_coastal <- plastic_waste %>% 
  mutate(coastal_pop_prop = coastal_pop / total_pop) %>%
  filter(plastic_waste_per_cap < 3)
ggplot (data= plastic_waste_coastal, 
        aes (x= coastal_pop_prop, y=plastic_waste_per_cap,))+
  geom_smooth( color= "black", size = 1)+
  geom_point(aes(color= continent))+
  labs(x="Proportion de la population côtière", y= "Nombre de déchets plastiques par habitant ", title="Quantité de déchet plastiques vs Proportion de la population côtière", subtitle="Selon le continent" )
```

    ## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

    ## Warning: Removed 10 rows containing non-finite outside the scale range
    ## (`stat_smooth()`).

    ## Warning: Removed 10 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](lab-02_files/figure-gfm/recreate-viz-1.png)<!-- --> On voit que plus
la population vivant sur les côtes est importante, plus la production de
plastique est élévé, il y a donc un lien direct entre la démographie et
la production de déchet plastique. On remarque quand même que certains
pays se situent en dessous de cette moyenne, ce qui montre un
comportement consomatif différent et on peut l’obreser aussi avec les
pays des continents. La majorité des pays africains se trouvent sous la
tendance alors que ceux de l’Amérique du Nord sont plus au dessus.
