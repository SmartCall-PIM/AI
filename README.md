
# SmartCall AI

Uma API simples em Python (FastAPI) que analisa descrições de chamados usando a API do Gemini (Google Generative AI) e retorna uma análise estruturada (título, categoria, prioridade e sugestão de solução).

## Recursos

- Recebe uma descrição de um chamado.
- Envia para o modelo Gemini e recebe uma análise em JSON.
- Retorna título, categoria, prioridade e sugestão de solução.

## Estrutura do projeto

- `api/` - Código da API (principal em `api/main.py`).
- `prompts.ini` - Templates de prompt usados para conversar com o Gemini.
- `LICENSE` - Licença do projeto.

## Pré-requisitos

- Python 3.10+ instalado
- Chave da API do Gemini (variável de ambiente `GEMINI_API_KEY`)

## Instalação rápida

1. Crie e ative um ambiente virtual (Windows PowerShell):

```powershell
python -m venv .venv; .\.venv\Scripts\Activate
```

2. Instale dependências (exemplo mínimo):

```powershell
pip install fastapi uvicorn google-generativeai python-dotenv
```

3. Defina a variável de ambiente ou crie um arquivo `.env` com a chave:

```
GEMINI_API_KEY=seu_token_aqui
```

4. Execute a API (modo desenvolvimento):

```powershell
uvicorn api.main:app --reload --host 0.0.0.0 --port 8000
```

## Endpoint principal

POST /analisar

Request JSON:

```json
{
	"descricao": "O computador não liga. Ao pressionar o botão, não há resposta e o LED não acende."
}
```

Resposta (exemplo):

```json
{
	"titulo": "PC não liga",
	"categoria": "Hardware",
	"prioridade": "Alta",
	"sugestao_solucao": "Verificar cabo de alimentação e fonte; testar com outra tomada; checar conexões internas."
}
```

Exemplo usando PowerShell para testar:

```powershell
Invoke-RestMethod -Uri "http://127.0.0.1:8000/analisar" -Method Post -Body (ConvertTo-Json @{ descricao = "O computador não liga" }) -ContentType "application/json"
```

> Observação: se a variável `GEMINI_API_KEY` não estiver configurada ou se houver problema com a integração, a API retornará erro 500 ao tentar analisar.

## Configuração do prompt

O template usado para construir a solicitação ao Gemini está em `prompts.ini` (seção `GeminiPrompts`, chave `chamado_ti`). Edite esse arquivo para ajustar o comportamento da análise.

## Licença

Este projeto está licenciado sob a mesma licença presente no arquivo `LICENSE`.

---

Se quiser, posso deixar o README mais detalhado (ex.: adicionar badges, exemplos de resposta reais, abrir um `requirements.txt` ou instruções para Docker). Diga o que prefere.
