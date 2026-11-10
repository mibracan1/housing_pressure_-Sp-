# Housing Pressure. Census tract level (Spain)

Data and code for mapping housing pressures and strategic planning.

A raw Pmtiles object is provided for easing data integration in web mapping apps

You can check out a previsualization here: https://mibracan1.github.io/housing_pressure_-Sp-/ 

## Data Sources 

**Income data** was retrieved from Instituto Nacional de Estadística employing *ineAtlas* R package created by [Pablo García Guzmán (@pablogguz)](https://github.com/pablogguz)
        García Guzmán P (2026). ineAtlas: Access to Spanish Household Income Distribution Atlas Data. R package version 0.2.1, https://github.com/pablogguz/ineAtlas.

**Rent data** was retrieved from SERPAVI
        Ministerio de Vivienda y Agenda Urbana (2026). Sistema Estatal de Referencia del Precio del Alquiler de Vivienda. https://www.mivau.gob.es/vivienda/alquila-bien-es-tu-derecho/serpavi [Accessed October 17, 2026]



## Data treatment 

The weighted average housing price is calculated using a straightforward weighted mean:

$$P_{\text{mean}} = \frac{(P_{\text{vc}} \cdot N_{\text{vc}}) + (P_{\text{vu}} \cdot N_{\text{vu}})}{N_{\text{total}}}$$

where $P_{\text{vc}}$ is the median monthly price for Multi-family Housing (Vivienda Colectiva), $P_{\text{vu}}$ is the median monthly price for Single-family Housing (Vivienda Unifamiliar), $N_{\text{vc}}$ and $N_{\text{vu}}$ are their respective counts, and $N_{\text{total}}$ is the total number of housing units.

The main objective of the web map is to channel strategic focus toward priority action areas within the housing affordability crisis.To achieve this, a composite index is developed to summarize the strategic relevance of each census section (sección censal). 

The areas of highest strategic priority are defined by two key factors: 
    (1) Higher rent-to-income burden: The proportion of median household income absorbed by rent payments.
    (2) Higher volume of active leases: The absolute count of registered rental contracts.
    
The index yields high values for census sections that simultaneously feature a high volume of active leases and significant housing cost pressure relative to median income.

This analytical design introduces three structural biases that must be accounted for:
    (1) Invisibilization of low-income areas: In lower-income census sections, the absolute count of formal rental contracts is often lower, even though the rent burden relative to local wages is extreme. In these instances, null values ($NaN$) or artificially low score outputs may occur.
    (2) Exclusion of total housing stock prices: The scope is strictly limited to the residential rental market rather than overall housing market prices.
    (3) Formal registration reliance: The index only captures officially registered tenancy contracts. 
    
This requires integrating estimation techniques and qualitative assessments when designing public intervention strategies.

Index Construction & Normalization

The input variables, both Number of Housing Units ($N$) and Residential Rent Burden ($P$)(defined as the percentage of median rent over median income) are normalized using a Min-Max transformation.  

The **Composite Index of Residential Pressure Areas** ($I_{\text{mult}, i}$) is aggregated via multiplication in order to penalize census sections that possess high housing volume but low rent burden, or vice versa:

$$I_{\text{mult}, i} = N_{\text{norm}, i} \times P_{\text{norm}, i}$$



## Author 

Miguel Bravo Candela 
