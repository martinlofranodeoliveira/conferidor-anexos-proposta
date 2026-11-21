# Conferidor de Anexos de Proposta

Compare os arquivos preparados com a lista esperada e confira ausências, extras e duplicatas por conteúdo.

## Como usar

Abra a [demonstração](https://martinlofranodeoliveira.github.io/conferidor-anexos-proposta/). Para uso local, execute `python3 -m http.server 8000` no diretório e abra `http://localhost:8000`.

Preencha a lista de documentos esperados. Selecione os arquivos no dispositivo para calcular SHA-256 no navegador ou preencha a lista de arquivos manualmente. Clique em **Conferir anexos** para identificar ausências, extras e cópias. O relatório está disponível em CSV.

## Contrato público

input deve ser objeto com expected (array de strings) e files (array de {name,sha256?}), ambos com até 100 entradas. Nomes são strings de 1 a 120 caracteres após trim, sem barra, contrabarra ou caracteres de controle. Compare por trim().toLowerCase(), preservando acentos. Dois esperados com o mesmo nome normalizado tornam o input inválido. sha256 ausente ou null não conta para duplicação de conteúdo. Se presente, deve ser uma string de 64 dígitos hexadecimais, comparados sem distinguir maiúsculas. Um input inválido retorna exatamente {error:"INVALID_INPUT"}.
Retorne {rows,summary}. Cada linha tem name (nome esperado após trim ou, nos extras, grafia após trim do primeiro arquivo daquele nome), occurrences (número de arquivos com aquele nome normalizado), status (MISSING se esperado e ausente, OK se esperado e presente, EXTRA se não esperado) e duplicateContent (true se algum arquivo dessa linha compartilha seu hash com outro arquivo, inclusive dentro da mesma linha). Liste esperados na ordem informada e extras pela primeira ocorrência. summary tem missing, extra, duplicateNames (linhas com occurrences>1) e duplicateContentGroups (quantidade de hashes não nulos distintos usados duas ou mais vezes).

## Escopo

Demonstração offline com exemplos fictícios. A equipe responsável avalia documentação, conformidade e habilitação. A interface processa os dados no navegador. O motor foi gerado com Gemini 4 Neon no Vertex AI.

## Testes

Execute `node scripts/test.mjs public.json`.

## Licença

MIT. Acorn preserva sua licença em scripts/vendor/LICENSE-Acorn.txt.
