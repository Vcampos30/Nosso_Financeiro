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
