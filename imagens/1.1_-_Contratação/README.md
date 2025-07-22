# Sistema de Migração de Imagens para Knowledge Base do Bedrock

Este sistema automatiza o processo de migração das imagens do Manual Loja Padrões para GitHub Pages e gera documentos otimizados para a Knowledge Base do Amazon Bedrock com posicionamento inteligente de imagens.

## 📋 Visão Geral

O sistema resolve o problema de imagens não acessíveis na Knowledge Base do Bedrock, migrando-as para o imgbb (serviço gratuito de hospedagem de imagens) e gerando documentos estruturados com as novas URLs.

## 🏗️ Estrutura do Projeto

```
├── imagens/                          # Imagens locais organizadas por categoria
│   ├── 1.1_-_Contratação/
│   ├── 1.2_-_Gestão_Pessoas/
│   └── ...
├── json imagens/                     # JSONs originais com metadados das imagens
│   ├── 1.1_-_Contratação.json
│   ├── 1.2_-_Gestão_Pessoas.json
│   └── ...
├── Manual Loja Padroes.pdf          # PDF original
├── setup_imgbb.py                   # Configuração da API imgbb
├── upload_images_to_imgbb.py        # Upload das imagens para imgbb
├── generate_kb_documents.py         # Geração de documentos para Bedrock
└── process_manual_complete.py       # Script principal
```

## 🚀 Como Usar

### Passo 0: Configurar Ambiente Virtual (Recomendado)

**Windows:**
```bash
setup_venv.bat
```

**Linux/Mac:**
```bash
chmod +x setup_venv.sh
./setup_venv.sh
```

**Ativar ambiente (após configuração):**
```bash
# Windows
activate_venv.bat

# Linux/Mac
source venv/bin/activate
```

**Verificar ambiente:**
```bash
python check_environment.py
```

### Passo 1: Preparar para GitHub Pages (Recomendado)

```bash
python prepare_manual_upload.py
```

Este script:
- Organiza imagens para upload manual no GitHub
- Cria estrutura completa do repositório
- Gera instruções detalhadas passo a passo
- Não requer Git CLI instalado

**Alternativa - API imgbb:**
```bash
python setup_imgbb.py
```

### Passo 2: Upload das Imagens

```bash
python upload_images_to_imgbb.py
```

Este script:
- Faz upload de todas as imagens locais para o imgbb
- Atualiza os JSONs com as novas URLs públicas
- Salva os JSONs atualizados na pasta `json_updated/`
- Aplica rate limiting para respeitar os limites da API

### Passo 3: Geração de Documentos

```bash
python generate_kb_documents.py
```

Este script:
- Gera documentos Markdown otimizados para Bedrock KB
- Gera documentos HTML para visualização
- Organiza o conteúdo com metadados estruturados
- Salva na pasta `bedrock_kb_docs/`

### Passo 4: Processo Completo (Alternativa)

```bash
python process_manual_complete.py
```

Script que executa todo o fluxo com verificações e relatórios.

## 📁 Estrutura de Saída

Após o processamento:

```
json_updated/                    # JSONs com URLs do imgbb
bedrock_kb_docs/
├── markdown/                   # Documentos .md para Bedrock KB
│   ├── 1.1_-_Contratação.md
│   ├── 1.2_-_Gestão_Pessoas.md
│   └── ...
└── html/                      # Documentos .html para visualização
    ├── 1.1_-_Contratação.html
    ├── 1.2_-_Gestão_Pessoas.html
    └── ...
```

## 📄 Formato dos Documentos Gerados

### Markdown (para Bedrock KB)

```markdown
# 1.1 Contratação

**ID do Processo:** 1.1_-_Contratação
**Tempo Padrão:** Não especificado

---

## Passo 1

**Página:** 1

Texto do passo...

### Imagens de Referência

**Imagem 1:** 1.1_-_Contratação_pagina_1_img_1.png
**Dimensões:** 495x700px
![1.1_-_Contratação_pagina_1_img_1.png](https://i.ibb.co/...)

```html
<img src="https://i.ibb.co/..." alt="Imagem do passo 1" style="max-width:100%; height:auto;">
```

---

## Metadados

- **Categoria:** Contratação
- **Subcategoria:** Gestão Gerencial
- **Total de Passos:** 8
- **Total de Imagens:** 45
```

### HTML (para visualização)

Documentos HTML responsivos com:
- Layout otimizado para visualização
- Grid de imagens responsivo
- Metadados organizados
- Estilos CSS incorporados

## 🔧 Configuração da API imgbb

### Obter API Key (Gratuito)

1. Acesse: https://api.imgbb.com/
2. Clique em "Get API Key"
3. Faça login ou crie uma conta
4. Copie sua API key

### Limites da API

- **Gratuito:** 100 uploads por hora
- **Tamanho máximo:** 32MB por imagem
- **Formatos:** JPG, PNG, BMP, GIF, WEBP, etc.
- **Hospedagem:** Permanente e gratuita

## 📊 Estatísticas do Manual

Com base na estrutura atual:

- **Total de categorias:** 27
- **Total de processos:** 27
- **Estimativa de imagens:** 500+
- **Tempo de processamento:** ~15-20 minutos

### Categorias Principais

1. **Gestão Gerencial** (1.x)
   - Contratação
   - Gestão de Pessoas
   - Estratégias e Resultados
   - Financeiro
   - Gestão de Riscos

2. **Execução Loja** (2.x)
   - Preparação e Execução
   - Estratégia
   - Precificação
   - Manutenção da Loja

3. **Gestão de Produtos** (3.x)
   - Insumos
   - Recebimento de Mercadoria
   - Reposição
   - EDL
   - Controle de Processos
   - Perdas
   - Preparação de Vendas

4. **Atendimento** (4.x)
   - Venda Balcão
   - Venda Salão
   - Venda Digital
   - Venda Manipulados
   - Serviço Farmacêutico
   - Atendimento Operador
   - Drive Thru
   - Furto

5. **Farmacêutico** (5.x)
   - Controle Farmácia

## 🎯 Integração com Bedrock

### Upload para Knowledge Base

1. Acesse o console do Amazon Bedrock
2. Vá para Knowledge Bases
3. Selecione sua KB ou crie uma nova
4. Faça upload dos arquivos `.md` da pasta `bedrock_kb_docs/markdown/`
5. Execute a sincronização

### Configuração do Agente

O agente agora poderá:
- Referenciar imagens diretamente nas respostas
- Mostrar screenshots dos processos
- Fornecer instruções visuais detalhadas
- Manter contexto visual durante o treinamento

### Exemplo de Resposta do Agente

```
Para o processo de contratação, siga estes passos:

1. Acesse o Portal Intranet -> Gerentes -> Merchandising

[Imagem mostrando a tela do portal]

2. Digite o nome da loja e clique OK

[Imagem mostrando o campo de entrada]

3. Baixe o template clicando em "Arquivo" -> "Baixar" -> "PowerPoint"

[Imagem mostrando o menu de download]
```

## 🔍 Troubleshooting

### Erro: "API key inválida"
- Verifique se copiou a API key corretamente
- Teste com `python setup_imgbb.py`

### Erro: "Limite de uploads excedido"
- Aguarde 1 hora (limite de 100 uploads/hora)
- Execute o script em lotes menores

### Erro: "Imagem não encontrada"
- Verifique se as pastas `imagens/` estão completas
- Confirme se os caminhos nos JSONs estão corretos

### Erro: "Falha no upload"
- Verifique conexão com internet
- Confirme se a imagem não está corrompida
- Tente novamente (o script pula imagens já processadas)

## 📈 Benefícios

### Para o Agente Bedrock
- Respostas mais ricas e visuais
- Melhor experiência de treinamento
- Redução de ambiguidade nas instruções
- Maior engajamento dos colaboradores

### Para a Operação
- Processo automatizado e escalável
- Imagens sempre acessíveis
- Backup das imagens em serviço confiável
- Documentação estruturada e pesquisável

### Para Manutenção
- Fácil atualização de imagens
- Versionamento de documentos
- Relatórios de processamento
- Estrutura modular e extensível

## 🔄 Atualizações Futuras

Para adicionar novos processos:

1. Adicione as imagens na pasta `imagens/`
2. Crie o JSON correspondente em `json imagens/`
3. Execute novamente os scripts
4. Faça upload dos novos documentos para o Bedrock

## 📞 Suporte

Para dúvidas ou problemas:
1. Verifique o arquivo `relatorio_processamento.txt`
2. Execute `python setup_imgbb.py` para testar a API
3. Consulte os logs de erro nos scripts
