## 📋 **PLANO DE REESTRUTURAÇÃO DO COMPILADOR**

Seu projeto já tem muitas peças, mas precisa de reorganização para seguir o pipeline do slide:

|**Componente**|**Status Atual**|**Ação Necessária**|
|---|---|---|
|Analisador Léxico|✅ Existe (`lexer.py`)|Padronizar interface|
|Analisador Sintático|✅ Existe (`parser.py`)|Integrar com AST Builder|
|AST Builder|⚠️ Misturado no parser|**Separar em módulo próprio**|
|Análise Semântica|✅ Existe (`semantic.py`)|Integrar com tabela de símbolos|
|Tabela de Símbolos|✅ Existe (`symbol_table.py`)|OK|
|Geração de IR|✅ Existe (`codegen.py`)|Renomear para `ir_generator.py`|
|Otimizador|❌ Não existe|**CRIAR**|
|Gerador Assembly|⚠️ Básico|**EXPANDIR**|
|Pipeline Integrado|⚠️ Parcial (`compiler_etapa7.py`)|**REFATORAR** completamente|

---

## 🚀 **PASSOS PARA REESTRUTURAÇÃO**

### **PASSO 1: Reorganizar Estrutura de Pastas**

bash

```bash
compilador-python/
├── README.md
├── requirements.txt
├── .gitignore
├── src/
│   ├── __init__.py
│   ├── lexer.py              # Analisador Léxico
│   ├── parser.py             # Analisador Sintático
│   ├── ast_builder.py        # ⭐ CRIAR - Construtor de AST
│   ├── semantic.py           # Analisador Semântico
│   ├── symbol_table.py       # Tabela de Símbolos
│   ├── ir_generator.py       # ⭐ RENOMEAR codegen.py
│   ├── optimizer.py          # ⭐ CRIAR - Otimizador
│   ├── codegen.py            # ⭐ RENOMEAR para assembly_generator.py
│   ├── runtime.py            # Runtime Stack (já existe)
│   ├── interpreter.py        # Interpretador (já existe)
│   └── compiler.py           # ⭐ CRIAR - Pipeline Principal
├── tests/
│   ├── test_lexer.py
│   ├── test_parser.py
│   ├── test_semantic.py
│   ├── test_ir.py
│   ├── test_optimizer.py
│   ├── test_codegen.py
│   └── test_pipeline.py      # ⭐ CRIAR - Teste integrado
├── examples/
│   ├── simple.txt
│   ├── functions.txt
│   └── optimizations.txt
└── docs/
    └── pipeline.md
```