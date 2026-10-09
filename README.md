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
- Leitura OCR de cupons e extração de faturas PDF ainda não implementadas. O seletor de arquivo é apenas um placeholder.
- Não há importação de extratos bancários nem conciliação automática ainda.
- A versão inicial é um protótipo funcional; valide os cálculos e mantenha backups.

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
