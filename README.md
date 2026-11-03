# iPhone — Simulador de parcelamento

Abra `index.html` no navegador. Funciona sem instalação, backend, internet ou bibliotecas externas. O filtro inicial mostra versões Pro; desmarque-o para acessar os 29 itens. Escolha o aparelho, ative a entrada se desejar e selecione de 1 a 12 parcelas. A tabela compara todos os prazos.

## Aparência e celular

O botão **Enviar pelo WhatsApp** abre `wa.me` com uma mensagem contendo a opção selecionada, preço, entrada, saldo, prazo, taxa, acréscimo e total (incluindo o ajuste da última parcela). O site publicado direciona ao contato configurado no secret `WHATSAPP_NUMBER`. Você confirma o envio no WhatsApp. Se houver uma entrada inválida, o botão fica indisponível. A opção de copiar permanece disponível.

No topo, escolha o tema Branco, Preto ou Automático (acompanha o sistema). A escolha é salva neste navegador quando o armazenamento local está disponível. No celular, o formulário e o resultado ficam em uma coluna, com controles maiores para toque. A comparação se transforma em cartões que cabem na tela, destacando o prazo selecionado.

## Dados

O rodapé exibe um contador global de acessos via [Hits](https://github.com/silentsoft/hits), iniciado em 03/11/2026. A contagem depende do carregamento da imagem externa: não recupera visitas anteriores nem representa visitantes únicos; bloqueadores, cache e disponibilidade do serviço podem afetá-la. O simulador e seus cálculos continuam funcionando se o contador estiver indisponível. O navegador faz uma solicitação ao serviço Hits para carregar o contador, sem enviar os dados da simulação.

Modelos, capacidades, cores, condições, preços e taxas foram fornecidos pelo usuário em 03/11/2026. As cores com o mesmo preço ficam agrupadas, preservando os 29 itens originais. Não houve consulta de disponibilidade ou validação comercial. Para atualizar, edite `products` e `rates` em `index.html`.

Taxas totais: 1x 5,81%; 2x 12,22%; 3x 13,62%; 4x 14,40%; 5x 15,33%; 6x 16,27%; 7x 17,63%; 8x 18,47%; 9x 19,32%; 10x 20,32%; 11x 21,79%; 12x 22,38%.

## Fórmula

- Saldo = preço − entrada.
- Acréscimo = saldo × taxa total do prazo, arredondado para centavos.
- Valor financiado = saldo + acréscimo.
- Parcela = valor financiado ÷ quantidade de parcelas.
- Total pago = entrada + valor financiado.

O cálculo usa centavos inteiros. As primeiras parcelas são truncadas em centavos e a última recebe o restante, sem alterar o total. Não são juros compostos mensais nem cálculo por divisão por (1 − taxa). Até 1x recebe a taxa informada. Entrada igual ao preço zera saldo, acréscimo e parcelas. Entradas negativas, superiores ao preço ou com mais de duas casas decimais são rejeitadas.

Exemplo: R$ 8.290,00 com R$ 2.000,00 de entrada em 12x: saldo R$ 6.290,00; acréscimo R$ 1.407,70; 11 parcelas de R$ 641,47 e última de R$ 641,53; total R$ 9.697,70.

## GitHub Pages

O GitHub Pages usa GitHub Actions (`.github/workflows/pages.yml`). Configure o secret de repositório `WHATSAPP_NUMBER` com DDI, DDD e número, somente dígitos. O workflow verifica os cálculos, executa `node build.cjs` e publica a pasta `dist`.

O número é mantido no secret na configuração, mas fica necessariamente público no HTML e no link do WhatsApp da versão publicada. Não use esta técnica para chaves privadas ou senhas. A configuração não envia mensagens automaticamente.

Para preparar a versão local com destinatário fixo, defina a variável de ambiente `WHATSAPP_NUMBER`, execute `node build.cjs` e abra `dist/index.html`. O `index.html` original sem preparação mantém o compartilhamento sem destinatário fixo. Alterações no secret exigem uma nova execução do workflow.

## Verificação

Execute `node verificar.cjs` para conferir catálogo, taxas, cálculos de todos os aparelhos/prazos, entrada integral e validações de entrada.
