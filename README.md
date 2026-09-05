# a11y-compiler
 
> Acessibilidade não deveria ser um plugin de lint que você esquece de instalar. Deveria ser um erro de compilação.
 
O **a11y-compiler** usa a **TypeScript Compiler API** para ler seus arquivos `.tsx`, transformá-los em uma AST e aplicar contratos de acessibilidade **antes** do seu código chegar em produção. Se o build passa, a acessibilidade básica da UI está garantida — não é uma sugestão, é uma regra.
 
## O que ele verifica
 
- 🖼️ **Imagens** — todo `<img>` precisa de `alt`. Sem exceções silenciosas.
- ⌨️ **Interação por teclado** — elementos clicáveis (`onClick`, `role="button"`, etc.) precisam ser navegáveis via teclado, não só via mouse.
- 🏷️ **Inputs** — todo campo de formulário precisa de um `label` associado, explícito ou via `aria-label`.
Cada regra é implementada como um *visitor* que percorre a AST procurando o padrão problemático — sem regex, sem heurística frágil em cima de string, análise real de estrutura de código.
 
## Comportamento
 
Ao rodar, o compilador analisa os arquivos-alvo e:
 
- ✅ Nenhuma violação → build segue normalmente.
- ❌ Alguma violação → reporta arquivo e linha, e finaliza com **exit code 1**.
Isso significa que ele se encaixa direto em CI/CD como um **gate de qualidade obrigatório**, não como um aviso que todo mundo ignora no terminal.
 
## Motivação
 
A maioria das ferramentas de acessibilidade hoje vive na periferia do processo de desenvolvimento: linters opcionais, extensões de VSCode, auditorias manuais que acontecem (ou não) antes do deploy. O **a11y-compiler** parte de uma provocação diferente:
 
> E se acessibilidade fosse tratada como responsabilidade da linguagem/compilador, e não de uma ferramenta de terceiros?
 
Colocar a verificação na etapa de compilação muda o incentivo: acessibilidade deixa de ser "boa prática" e passa a ser **contrato de código** — quebrou o contrato, não builda.
 
## Status
 
🚧 Fase conceitual/inicial. Próximos passos:
 
- [ ] Expandir o conjunto de regras (contraste de cor, ordem de foco, `aria-*` semântico)
- [ ] Publicar como pacote instalável via npm
- [ ] Escrever casos de teste cobrindo falsos positivos/negativos
- [ ] Definir posicionamento no portfólio, junto com estudos de acessibilidade web já feitos
 
