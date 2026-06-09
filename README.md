# Ransomware 

Um projeto educacional que demonstra como funciona criptografia de arquivos, implementando um sistema de cifra simétrica com a biblioteca Fernet. **PROJETO EXCLUSIVAMENTE PARA FINS EDUCACIONAIS.**

##  AVISO LEGAL CRÍTICO

**Este projeto é APENAS para fins educacionais de pesquisa de segurança defensiva.**

O uso não autorizado deste software para:
- Criptografar arquivos de terceiros sem consentimento
- Extorquir resgate (ransomware)
- Destruir ou inacessibilizar dados
- Causar danos econômicos
- Chantagem ou extorsão

**É CRIME E TERRORISMO CIBERNÉTICO com penas severas:**
-  **Prisão de 5 a 20 anos**
-  **Multas de milhões de dólares**
-  **Antecedentes criminais permanentes**
-  **Processos criminais federais**
-  **Perseguição internacional**

**O ransomware custou bilhões em danos globalmente. NUNCA use este código maliciosamente.**

##  Descrição

Este projeto implementa um sistema educacional de criptografia e descriptografia de arquivos usando o algoritmo Fernet (criptografia simétrica). O propósito é entender como os dados podem ser protegidos criptograficamente e, inversamente, como o ransomware funciona para fins de defesa.

##  Conceitos Educacionais

- ✅ Entender criptografia simétrica
- ✅ Aprender sobre algoritmo Fernet
- ✅ Gerenciamento de chaves criptográficas
- ✅ Operações com arquivos em modo binário
- ✅ Mecanismos de ransomware (defensiva)
- ✅ Importância de backups e segurança

##  Requisitos

- **Python 3.6+**
- **cryptography** - Biblioteca criptográfica

### Instalação de dependências

```bash
pip install cryptography
```

##  Estrutura de Arquivos

```
ransomware/
├── criptografia.py          # Script para criptografar arquivos
├── descriptografia.py       # Script para descriptografar arquivos
├── keys/                    # Diretório para armazenar chaves
│   └── chave.key           # Chave simétrica gerada
└── README.md
```

##  Como Funciona - Criptografia Simétrica

### O que é Fernet?

Fernet é um protocolo de criptografia simétrica que:
- Usa a **mesma chave** para cifrar e decifrar
- Combina **AES-128** com **HMAC** para autenticação
- Garante **confidencialidade e integridade**
- Usa **tokens com timestamp** para reutilização de chaves

### Fluxo de Criptografia

```
Arquivo Original (Legível)
         ↓
    Chave Fernet
         ↓
   Algoritmo AES-128
         ↓
    Adiciona HMAC
         ↓
Arquivo Criptografado (Ilegível)
```

##  Uso (Ambiente Educacional Controlado)

### 1. Gerar Chave Criptográfica

```python
from cryptography.fernet import Fernet

key = Fernet.generate_key()
print(key)  # Exemplo: b'kO7EKp...vZ9dQ='
```

### 2. Salvar a Chave

```python
with open("keys/chave.key", 'wb') as f:
    f.write(key)
```

### 3. Criptografar um Arquivo

```bash
# Editar criptografia.py:
# 1. Adicionar arquivo à lista 'files'
files = ["documento.txt"]

# 2. Executar:
python criptografia.py

# Resultado: documento.txt agora está criptografado
```

### 4. Descriptografar o Arquivo

```bash
# Editar descriptografia.py:
# 1. Adicionar arquivo à lista 'files'
files = ["documento.txt"]

# 2. Executar:
python descriptografia.py

# Resultado: documento.txt volta ao estado original
```

##  Estrutura do Código

### `criptografia.py`

```python
# Gera uma nova chave
key = Fernet.generate_key()

# Salva a chave em arquivo
with open("keys/chave.key", 'wb') as chave:
    chave.write(key)

# Para cada arquivo:
# 1. Lê o arquivo em modo binário
# 2. Criptografa o conteúdo com Fernet
# 3. Sobrescreve o arquivo com dados criptografados
```

**Fluxo:**
```
Arquivo Original
    ↓
Lê em binário (rb)
    ↓
Criptografa com Fernet
    ↓
Escreve em binário (wb)
    ↓
Arquivo Ilegível
```

### `descriptografia.py`

```python
# Carrega a chave do arquivo
with open("keys/chave.key", 'rb') as chave:
    key = chave.read()

# Para cada arquivo:
# 1. Lê o arquivo criptografado em modo binário
# 2. Descriptografa o conteúdo com Fernet
# 3. Sobrescreve o arquivo com dados originais
```

**Fluxo:**
```
Arquivo Criptografado
    ↓
Lê em binário (rb)
    ↓
Descriptografa com Fernet
    ↓
Escreve em binário (wb)
    ↓
Arquivo Original
```

##  Gerenciamento de Chaves

###  CRÍTICO: Proteção da Chave

A segurança depende **completamente** da chave:

```python
#  NUNCA faça isso:
key = "minha_chave_123"  # Hardcoded - INSEGURO!

#  SEMPRE faça isso:
with open("keys/chave.key", 'rb') as f:
    key = f.read()  # Armazenada separadamente

#  MELHOR ainda:
import os
key = os.environ.get('ENCRYPTION_KEY')  # Variável de ambiente
```

### Perda da Chave

- **Se perder a chave:** Dados são irrecuperáveis (mesmo para proprietários)
- **Se roubarem a chave:** Dados podem ser descriptografados
- **Ransomware rouba a chave:** Demanda resgate por chave e descriptografia

##  Tamanho de Dados

Fernet adiciona overhead:

```
Arquivo original: 100 bytes
Arquivo criptografado: 154 bytes (54 bytes de overhead)

Overhead = Timestamp (8) + Versão (1) + IV (16) + HMAC (32) + Padding
```

##  Diferenças: Criptografia vs Ransomware

| Aspecto | Criptografia Legítima | Ransomware |
|---------|----------------------|-----------|
| **Propósito** | Proteger dados próprios | Extorquir vítimas |
| **Chave** | Armazenada seguramente | Armazenada remotamente |
| **Consentimento** | Próprio usuário | Sem consentimento |
| **Acesso** | Titular tem acesso | Acesso negado |
| **Intenção** | Confidencialidade | Extorsão/Dano |
| **Legalidade** | Legal | ILEGAL |

##  Como Funciona Ransomware Real

1. **Infecção** - Malware entra no sistema
2. **Descoberta** - Identifica arquivos valiosos
3. **Criptografia** - Criptografa com chave remota
4. **Nota de Resgate** - Deixa instrução de pagamento
5. **Espera** - Aguarda vítima pagar
6. **Descriptografia** - Fornece chave (se pagar)

## 🛡️ Proteção Contra Ransomware

### Defesa Preventiva
- ✅ Manter software atualizado
- ✅ Usar antivírus/anti-malware
- ✅ Não abrir emails suspeitos
- ✅ Desativar macros do Office
- ✅ Usar firewall
- ✅ Educação de usuários

### Defesa de Dados
- ✅ Backups automáticos e regulares
- ✅ Backups offline (desconectados)
- ✅ Múltiplas cópias
- ✅ Teste de recuperação
- ✅ Histórico de versões

### Se Infectado
- ✅ Isolar o computador da rede
- ✅ NÃO pagar resgate (não garante descriptografia)
- ✅ Reportar à polícia
- ✅ Restaurar de backup
- ✅ Usar ferramentas de descriptografia (algumas existem)

##  Conceitos de Segurança

### Criptografia Simétrica (Fernet)
- Uma chave para cifrar E decifrar
- Rápida e eficiente
- Requer distribuição segura da chave

### Criptografia Assimétrica
- Chave pública para cifrar
- Chave privada para decifrar
- Mais segura para distribuição

### HMAC (Hash-based Message Authentication Code)
- Verifica integridade dos dados
- Detecta modificações
- Previne ataques de tampering

##  Sinais de Infecção por Ransomware

- Arquivos renomeados com extensão desconhecida (.encrypted, .locked, etc)
- Nota de resgate em cada pasta (README.txt, .html)
- Computador muito lento
- Programas não abrem
- Tela de bloqueio com demanda de resgate
- Comunicação de rede suspeita

##  Checklist de Segurança

- [ ] NUNCA use este código em máquinas alheias
- [ ] Use apenas em seus próprios arquivos para teste
- [ ] Mantenha backup dos arquivos ANTES de testar
- [ ] Armazene chaves em local seguro
- [ ] Nunca compartilhe chaves privadas
- [ ] Use para aprender sobre defesa
- [ ] Respeite a lei e propriedade alheia

##  Recursos Educacionais

- [OWASP - Cryptography](https://owasp.org/)
- [Cryptography.io - Fernet](https://cryptography.io/en/latest/fernet/)
- [FBI - Ransomware](https://www.fbi.gov/investigate/cyber)
- [CISA - Ransomware Alerts](https://www.cisa.gov/)

##  Licença

Este projeto não possui licença especificada.

##  Autor

[deVictorS](https://github.com/deVictorS)

---

##  AVISO FINAL - LEIA COM ATENÇÃO

**Este código é fornecido APENAS para fins educacionais e de pesquisa defensiva.**

### O Que NÃO Fazer:
- ❌ Usar em máquinas alheias
- ❌ Criptografar dados sem permissão
- ❌ Exigir resgate por descriptografia
- ❌ Distribuir como malware
- ❌ Usar para chantagem

### Consequências Legais:
- Processos criminais federais
- Acusação sob Computer Fraud and Abuse Act (EUA)
- Acusação sob Lei de Crimes Cibernéticos (Brasil)
- Penas de prisão de 5+ anos
- Multas de milhões de dólares
- Responsabilidade civil

**O ransomware é a ameaça #1 a negócios mundialmente. Use seu conhecimento para PROTEGER, nunca para PREJUDICAR.**

**Sua responsabilidade: Não use este conhecimento para fins maliciosos.**
