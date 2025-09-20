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
         aes(x = plastic_waste_per_cap)) +
  geom_histogram(binwidth = 0.2)+
    labs(x= "quantité de plastique non gérés", y = "continent" )
```

![](lab-02_files/figure-gfm/filter-data-1.png)<!-- -->

## Exercices

### Exercise 1

``` r
# insert code here
ggplot(data = plastic_waste,
       aes(x= plastic_waste_per_cap))+
  geom_histogram(binwidth = 0.2)+
  labs(x= "quantité de plastique non gérés", y = "continent" )+
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
# insert code here
ggplot(data = plastic_waste,
       aes(x= plastic_waste_per_cap, color = continent, fill = continent))+
  geom_density(size= 0.15,alpha= 0.5)
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
# insert code here
```

Violin plot:

``` r
# insert code here
```

Réponse à la question…

### Exercise 4

``` r
# insert code here
```

Réponse à la question…

### Exercise 5

``` r
# insert code here
```

``` r
# insert code here
```

Réponse à la question…

## Conclusion

Recréez la visualisation:

``` r
# insert code here
```
