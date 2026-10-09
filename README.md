# Nosso Financeiro — PWA local (V1)

## O que já funciona
- Painel mensal com renda familiar, gastos, saldo estimado e compromissos futuros.
- Cadastro, edição e exclusão de gastos.
- Categorias editáveis.
- Cadastro de renda líquida por pessoa e competência.
- Cartões individuais.
- Contas recorrentes com vencimento e estado pago/pendente.
- Parcelas planejadas em compras parceladas no cartão de crédito.
- Histórico mensal, filtros, resumo individual, médias e gráficos simples.
- Exportação de backup JSON e CSV de gastos.
- Importação de backup JSON (substitui os dados locais).
- Estrutura de PWA e cache para uso offline após primeiro carregamento.

## Limitações conhecidas desta V1
- Armazenamento é local por navegador/dispositivo; não existe sincronização automática.
- Backup JSON pode ser exportado e enviado pelo iCloud Drive e importado no outro dispositivo.
- Leitura de cupons por imagem/PDF com OCR e revisão editável de produtos, categorias, data e total.
- Importação de fatura/extrato PDF com extração heurística de lançamentos e tela de revisão; os formatos variam por banco e podem exigir ajustes.
- OCR e leitura de PDF carregam bibliotecas externas por CDN e podem exigir conexão com a internet na primeira utilização.
- A detecção de duplicidade é heurística e sempre deve ser revisada; não é uma integração bancária oficial.
- A versão inicial é um protótipo funcional; valide os cálculos e mantenha backups.

## Leitura de documentos
- Em Adicionar, use **Ler cupom fiscal** para foto ou PDF de cupom.
- Use **Ler fatura/extrato PDF** para tentar extrair lançamentos de um PDF bancário.
- Revise e corrija os campos antes de confirmar. OCR pode errar nomes, datas, valores e sinal de crédito/débito.
- PDFs protegidos por senha ou com layout incomum podem não ser reconhecidos.

## Como usar
1. Extraia o ZIP.
2. Para testar no computador, abra `index.html`. Algumas funções de PWA/offline só funcionam servidas por HTTPS ou localhost.
3. Para instalar no iPhone, publique a pasta em uma hospedagem estática HTTPS (por exemplo, GitHub Pages).
4. No Safari do iPhone, abra a URL publicada, toque em Compartilhar e selecione **Adicionar à Tela de Início**.
5. Para compartilhar dados entre aparelhos, vá a Configurações → Exportar backup JSON. Salve em Arquivos/iCloud Drive. No outro aparelho, abra o PWA e use Importar backup.

## Segurança e privacidade
Os dados financeiros são guardados no `localStorage` deste navegador. Limpar dados do site pode apagá-los. Faça backups frequentes. Não registre senhas bancárias ou números completos de cartão.

## Publicar no GitHub Pages
- Crie um repositório e envie `index.html`, `manifest.json`, `sw.js` e `icon.svg` para a raiz.
- Em Settings → Pages, escolha a branch principal e a pasta `/ (root)`.
- Aguarde a publicação e abra a URL HTTPS no Safari.


## Mesclagem inteligente de backups (V3)

- A importação não substitui os dados locais: mescla os registros do backup com os registros já existentes.
- Cada lançamento com ID já presente é ignorado, evitando repetir dados quando o mesmo backup circula entre os dois dispositivos.
- Categorias são reconciliadas pelo nome normalizado; cartões podem ser reconhecidos pelo nome e titular.
- Gastos, rendas, parcelas e contas são comparados por data/competência, valor e descrição para apontar possíveis duplicidades.
- Possíveis duplicidades aparecem em uma revisão. Por padrão, são ignoradas; o usuário pode marcar uma linha para importar também se forem dois lançamentos legítimos.
- Os nomes das duas pessoas configurados localmente são preservados durante a mesclagem.
- O algoritmo é heurístico: descrições diferentes para a mesma compra podem escapar, e compras legítimas iguais podem ser sinalizadas. Revise a lista antes de confirmar.


## Ajustes V4

- Rendas aparecem em uma lista da competência selecionada, com ações para editar e excluir.
- O campo de valor da renda aceita digitação livre e vírgula decimal para facilitar correções.
- Forma de pagamento inclui "Cartão Benefício".
- A categoria padrão "Higiene pessoal" foi renomeada para "Higiene", inclusive nos dados existentes.
- Categorias personalizadas continuam disponíveis em Configurações > Categorias, depois das categorias padrão (incluindo "Outros").
- Compras no cartão de crédito parceladas passam a contar nos gastos mensais como parcelas individuais, distribuídas mês a mês a partir do mês da compra. A compra integral deixa de ser somada toda na competência inicial; análises e lista mensal usam o valor de cada parcela.


## Ajustes V5 — análise financeira ampliada

- Os nomes dos integrantes são editáveis em Configurações. Novas instalações começam com "Integrante 1" e "Integrante 2"; os dados existentes são preservados, e os nomes padrão antigos são migrados para esses nomes genéricos.
- A área de Análises ganhou seletor de histórico (6, 12, 24 meses ou todo o histórico), indicadores de renda, gastos, saldo, taxa de poupança, média mensal, valor médio por lançamento, maior gasto e compromissos futuros.
- Inclui gráficos em barras de fluxo de caixa e renda versus gastos, composição por categoria e forma de pagamento, comparativo por integrante, maiores despesas, observações automáticas e projeção dos próximos três meses.
- As projeções usam média e tendência linear dos meses recentes, comparadas aos compromissos já cadastrados. A confiança indicada é baixa quando há poucos dados; não são garantias nem aconselhamento financeiro.


## Versão 6 — ajustes de navegação e gráficos
- Acesso permanente a **Ajustes** pela barra inferior; Configurações não fica mais escondida na tela Adicionar.
- Nomes dos integrantes editáveis em **Ajustes → Quem usa o aplicativo**, com atualização dos filtros e rótulos em toda a interface.
- A página Análises agora exibe gráficos SVG reais e responsivos: linha de saldo mensal, barras comparando renda e gastos e rosca da distribuição por categoria. Os gráficos são gerados com os lançamentos locais e não dependem de biblioteca externa.
- A versão continua usando armazenamento local do navegador; faça backup JSON antes de substituir arquivos.


## Versão final — período e identidade visual
- Central de Análises abre por padrão em **Últimos 30 dias**, com opção de **Últimos 3 meses** e demais períodos históricos.
- No recorte de 30 dias, despesas e parcelas são filtradas pela data real. Como a renda é registrada por competência mensal, a renda exibida corresponde ao mês atual; a própria tela informa essa limitação.
- Novo ícone aprovado: símbolo minimalista de casal e crescimento financeiro em verde profundo e dourado. Atualizados o ícone do app, favicon e Apple touch icon; o restante da interface não foi alterado.
- Cache do service worker atualizado para V7.
