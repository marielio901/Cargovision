# CargoVision

CargoVision é um painel web em Flask para monitoramento logístico com dados simulados: KPIs de SLA, mapa em tempo real com veículos/entregas, cadastro de pedidos e simulações rápidas de custo. O projeto usa SQLite e já vem com um conjunto de dados demo para testes.

## Principais recursos
- Dashboard operacional com indicadores de pedidos, SLA, atrasos e eventos de rastreamento.
- Mapa em tempo real (Leaflet) com frota, entregas, heatmap de risco e traçado de rotas.
- Cadastro de pedidos com coordenadas de destino, janelas de entrega e SLA.
- Simulações de custo por cenário (combustível, pedágio, distância, custo/km) e visualização de previsão de demanda.
- Perfis de acesso (admin, gestor, operador) e autenticação simples via Flask.

## Pré-requisitos
- Python 3.11+ (recomendado 3.11 ou 3.12)
- pip

## Como rodar localmente
1) Crie e ative um ambiente virtual:
```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
```
2) Instale as dependências:
```bash
pip install -r requirements.txt
```
3) Gere o banco SQLite com dados de exemplo:
```bash
python scripts/init_db.py
```
4) Inicie a aplicação:
```bash
python app.py
# ou, se preferir:
# flask --app app.py run
```
5) Acesse http://127.0.0.1:5000 no navegador.

## Usuários demo
- admin@cargovision.local / admin123
- gestor@cargovision.local / gestor123
- operador@cargovision.local / operador123

## Scripts úteis
- `python scripts/init_db.py` – cria `instance/cargovision.sqlite` e popula com frota, pedidos, eventos e previsões.
- `python scripts/simulate_tracking.py` – gera novos eventos de rastreamento aleatórios para viagens em rota (útil para manter o mapa se atualizando).

## Estrutura do projeto
- `app.py` – ponto de entrada Flask.
- `cargovision/` – blueprints (auth, cadastros, monitoramento, simulações), serviços e templates.
- `cargovision/static/` – CSS customizado, JS do mapa e assets do front-end.
- `scripts/` – inicialização do banco e simulador de telemetria.
- `instance/` – arquivo SQLite gerado em tempo de execução.

## Observações
- O banco fica em `instance/cargovision.sqlite`. Se precisar recriar os dados demo, rode novamente `python scripts/init_db.py`.
- O mapa recarrega camadas a cada 15s; execute o simulador para ver eventos recentes chegando.
