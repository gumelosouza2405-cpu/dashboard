# Visão de vendas — Dashboard interativo

Dashboard estático para explorar as vendas da hamburgueria, desenvolvido para a atividade de Fundamentos de IA e Análise de Dados com HTML, CSS e JavaScript puro.

## Abrir e usar

A imagem de Lionel Messi no banner é uma ilustração gerada por IA, usada como cena fictícia; não representa apoio ou parceria com o estabelecimento. Fonte da ilustração: [Easy-Peasy.AI](https://easy-peasy.ai/ai-image-generator/images/male-soccer-player-enjoying-burger-costa-rica-paradise).

1. Abra `public/index.html` no navegador. A demonstração inicial está incorporada no JavaScript, então não depende de `fetch` nem de um servidor local. As bibliotecas e a fonte tipográfica são carregadas por CDN e exigem conexão com a internet.
2. Use o período, a categoria e o segmento para filtrar os indicadores, os gráficos e a tabela. Pesquise ou ordene os registros pelas colunas; use os controles no rodapé da tabela para navegar pelas páginas.
3. Clique em **Importar CSV** para selecionar um arquivo no computador. O conteúdo é processado localmente no navegador e substitui a demonstração.
4. **Limpar filtros** restaura o período completo e remove categoria, segmento e pesquisa. **Exportar CSV** baixa os registros que correspondem aos filtros e à pesquisa atual, com a coluna calculada `faturamento`.

O CSV deve ter cabeçalho e as colunas `id_venda`, `data`, `produto`, `categoria`, `quantidade` e `preco_unitario`. Nomes equivalentes comuns (como `id`, `qtd`, `price` ou `date`) também são reconhecidos. Para o recorte de comparação, o dashboard usa `regiao` quando disponível; sem ela, usa `canal` e identifica essa adaptação, ou mostra um segmento genérico. Datas ISO `AAAA-MM-DD` são recomendadas; datas `DD/MM/AAAA` também são aceitas. Quantidade deve ser positiva e preço não negativo. Linhas sem ID, data válida ou números utilizáveis são ignoradas e contabilizadas na interface. Categoria, produto e segmento ausentes são exibidos como “Não informado”.

## Dados e regras da análise

O projeto já continha `vendas_hamburgueria.csv`, com 1.367 registros e campos adicionais como dia da semana, período, forma de pagamento, tempo de espera e avaliação. O arquivo original foi preservado. A cópia `public/dados-exemplo.csv` e a demonstração embutida correspondem a essa base.

Esta base cobre 1º de julho a 30 de setembro de 2026, não 12 meses; como havia uma base de vendas no projeto, ela foi usada em vez de criar dados fictícios. Ela não contém `regiao`, mas tem `canal` (`Delivery` e `Balcão`); por isso, o terceiro gráfico e o filtro comparam canais, explicitamente identificados na interface. As colunas adicionais da base são preservadas no arquivo de origem e não alteram as métricas do painel.

- Faturamento da linha: `quantidade × preco_unitario`.
- Faturamento total: soma do faturamento das linhas após filtros de período, categoria e segmento.
- Quantidade de vendas: número de `id_venda` únicos nas linhas filtradas.
- Unidades vendidas: soma das quantidades filtradas.
- Ticket médio: faturamento total dividido pela quantidade de vendas; quando não há vendas, o valor é R$ 0,00.

### Galeria de lanches

A galeria apresenta os produtos classificados como `Lanche`. As imagens s?o ilustrativas, servidas por `images.unsplash.com` e precisam de internet. Cr?ditos: [X-Bacon ? Jonathan Borba](https://unsplash.com/fr/photos/burger-avec-galette-bacon-et-fromage-xUtkfr-qBFU), [X-Tudo ? Fidel Fernando](https://unsplash.com/photos/plate-of-hamburger-xrdbUgwGWfo), [X-Burger ? amirali mirhashemian](https://unsplash.com/pt-br/fotografias/hamburguer-com-queijo-e-alface-9Bqiusimq6M) e [X-Salada ? Or Hakim](https://unsplash.com/photos/burger-with-lettuce-and-tomato-qJzlP_hqPEQ).

## Publicar no Render pelo GitHub

Envie o projeto para um repositório GitHub e, no Render, crie um serviço **Static Site** conectado ao repositório:

- **Tipo de serviço:** Static Site
- **Branch:** a branch que contém o projeto (por exemplo, `main`)
- **Root Directory:** vazio
- **Build Command:** `echo "Site pronto"`
- **Publish Directory:** `public`

O site não usa backend, banco de dados ou etapa de compilação. Chart.js, Papa Parse e as fontes do Google Fonts vêm de CDNs e precisam de internet para carregar.
