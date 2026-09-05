# a11y-compiler
Ferramenta que usa a TypeScript Compiler API para analisar arquivos .tsx, gerar a AST e aplicar contratos de acessibilidade em tempo de build.

## O que ele verifica
 
- **Imagens**: presença do atributo `alt`
- **Interação por teclado**: elementos interativos precisam ser navegáveis via teclado
- **Inputs**: presença de `label` associado
