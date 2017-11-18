---
title: Lab 01 - Parte 03
draft: false
---

Em todos os casos optei por usar a mediana por ser uma medida mais robusta e não sofrer com os efeitos dos outliers tal como a média.

## O que aconteceu com o volume percentual do açude depois que eu vim morar aqui em Campina Grande(em 2011)?
Para minha tristeza, o volume só diminuiu. Teria isso alguma 
correlação com a minha vinda? Eu diria que não, pois nunca fui 
alguém que gasta muita água, seja com o que for. Diria que tem muito mais a ver com a falta de chuvas do 
que com a minha vinda.

<div id="vis" width=300></div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/vega/3.0.7/vega.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/vega-lite/2.0.1/vega-lite.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/vega-embed/3.0.0-rc7/vega-embed.js"></script>
<script>
    const spec = {
    "$schema": "https://vega.github.io/schema/vega-lite/v2.json",
    "data": {
        "url": "https://api.insa.gov.br/reservatorios/12172/monitoramento",
        "format": {
        "type": "json",
        "property": "volumes",
        "parse": {
            "DataInformacao": "utc:'%d/%m/%Y'"
                }
            }
        },

    "height": 260,
	"width": 1024,
	"mark": "line",
	"encoding": {
	  "x": {
		"timeUnit": "year",
		"field": "DataInformacao",
		"type": "temporal",
		"format": "%Y",
		"axis": {"title": "Ano", "grid": false}
	  },
	  "y": {
		"field": "VolumePercentual",
		"aggregate": "median",
		"type": "quantitative",
		"axis": {"title": "Mediana do volume percentual", "grid": false}
	  }
	},
	"height": 260,
	"width": 720,
	"mark": "line",
	"encoding": {
	  "x": {
		"timeUnit": "yearmonth",
		"field": "DataInformacao",
		"type": "temporal",
		"format": "%Y",
		"axis": {"title": "Ano", "grid": false}
	  },
	  "y": {
		"field": "VolumePercentual",
		"aggregate": "median",
		"type": "quantitative",
		"axis": {"title": "Mediana do volume percentual", "grid": false}
	  }
	},
	"transform": [
		{"filter": {"timeUnit": "year", "field": "DataInformacao", "range": [2011, 2017] }}
		]
     };
     vegaEmbed('#vis', spec, {"actions": {export: false, source: false, editor: false}}).catch(console.warn);
</script>


## Levando em conta que o volume só diminuiu com a minha vinda para Campina Grande, durante que período a água chegou ao ponto de ficar em até 5% da capacidade no quesito volume percentual?
A visualização em questão responde essa pergunta. É interessante refletir sobre 
esse acontecimento. Penso que ninguém imaginaria que um açude dessa 
magnitude e importância alcançaria uma situação tão catastrófica.
Acredito que é possível extrair uma lição: até algo gigantesco como 
um açude pode ficar a beira de secar. Em outras palavras: muitas 
coisas na vida que pensamos ser inesgotáveis podem, de um momento para 
outro, esgotar quase que por completo. Relembrando aqui: claro que eu tenho participação na diminuição do volume, mas não como a 
coincidência evidenciada na visualização anterior faz crer(é melhor que ninguém saiba disso, pois posso ser linchado ou apelidado de "seca açude").


<div id="vis2" width=300></div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/vega/3.0.7/vega.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/vega-lite/2.0.1/vega-lite.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/vega-embed/3.0.0-rc7/vega-embed.js"></script>
<script>
    const spec2 = {
    "$schema": "https://vega.github.io/schema/vega-lite/v2.json",
    "data": {
        "url": "https://api.insa.gov.br/reservatorios/12172/monitoramento",
        "format": {
        "type": "json",
        "property": "volumes",
        "parse": {
            "DataInformacao": "utc:'%d/%m/%Y'"
                }
            }
        },

    "height": 260,
	"width": 720,
	 "mark": {"type": "bar", "filled": true},
	"encoding": {
	  "x": {
		"timeUnit": "yearmonth",
		"field": "DataInformacao",
		"type": "temporal",
		"axis": {"title": "Ano", "grid": false}
	  },
	  "y": {
		"field": "VolumePercentual",
		"aggregate": "median",
		"type": "quantitative",
		"axis": {"title": "Mediana do volume percentual", "grid": false}
	  }
	},
	"transform": [
		{"filter": {"field": "VolumePercentual", "range": [0.0, 5.0]}}
	]
    };
    vegaEmbed('#vis2', spec2, {"actions": {export: false, source: false, editor: false}}).catch(console.warn);
</script>

## E o contrário: durante que período a água chegou ao ponto de ficar em até 95% da capacidade no quesito volume percentual?
Em contraste, seria interessante 
ver o outro lado da moeda, ou seja, 
os momentos em que o açude esteve praticamente 
cheio. Aqui, considerei como critério para 
"quase cheio" está com, pelo menos, 95% do volume percentual. O legal de usar uma visualização através de gráfico de área é pelo fato 
de estarmos falando de quantidade de água e o gráfico se assemelhar um pouco com o açude tendo algumas ondulações.

<div id="vis3" width=300></div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/vega/3.0.7/vega.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/vega-lite/2.0.1/vega-lite.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/vega-embed/3.0.0-rc7/vega-embed.js"></script>
<script>
    const spec3 = {
    "$schema": "https://vega.github.io/schema/vega-lite/v2.json",
    "data": {
        "url": "https://api.insa.gov.br/reservatorios/12172/monitoramento",
        "format": {
        "type": "json",
        "property": "volumes",
        "parse": {
            "DataInformacao": "utc:'%d/%m/%Y'"
                }
            }
        },

    "height": 260,
	"width": 720,
	"mark": "area",
	"encoding": {
	  "x": {
		"timeUnit": "yearmonth",
		"field": "DataInformacao",
		"type": "temporal",
		"axis": {"title": "Ano", "grid": false}
	  },
	  "y": {
		"field": "VolumePercentual",
		"aggregate": "median",
		"type": "quantitative",
		"axis": {"title": "Mediana do volume percentual", "grid": false}
	  }
	},
	"transform": [
		{"filter": {"field": "VolumePercentual", "range": [95, 100]}}
		]
    };
    vegaEmbed('#vis3', spec3, {"actions": {export: false, source: false, editor: false}}).catch(console.warn);
</script>
