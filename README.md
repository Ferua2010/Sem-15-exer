# Conceitos Fundamentais e Checklist de Qualidade — Laravel

> **Nota:** Todos os exercícios práticos correspondentes aos tópicos listados a seguir já foram devidamente implementados e inseridos no código-fonte do projeto.

---

## 1. Conceitos de Desenvolvimento

1. **Semântica RESTful:** `GET` deve apenas consultar dados. Usá-lo para excluir é perigoso porque robôs de busca podem acessar o link automaticamente e apagar registros.
2. **Idempotência:** Significa que repetir uma requisição produz o mesmo efeito final. `PUT` é idempotente porque mantém o mesmo estado; `POST` pode criar novos registros a cada envio.
3. **Resource Controllers:** As sete ações são `index` (listar), `create` (formulário de cadastro), `store` (salvar), `show` (detalhar), `edit` (formulário de edição), `update` (atualizar) e `destroy` (excluir).
4. **Injeção de Dependências:** Ao declarar `Request $request`, o Service Container entrega automaticamente a requisição atual ao controller, sem precisar de `new Request()`.
5. **Method Spoofing:** Formulários HTML convencionais usam `GET` ou `POST`. O Laravel utiliza `@method('PUT')`, `@method('PATCH')` ou `@method('DELETE')` para indicar o verbo desejado.
6. **CSRF:** É um ataque que tenta executar ações em nome de um usuário autenticado. `@csrf` adiciona um token ao formulário, que o Laravel compara com o token da sessão.
7. **Constraints de Rota:** Restringem o formato dos parâmetros, como apenas números ou caracteres alfanuméricos. Quando o formato não corresponde, o Laravel retorna status `404`.
8. **Rotas Nomeadas:** Facilitam mudanças nas URLs sem alterar todas as views e tornam o código mais legível, reduzindo erros em links.
9. **Single Responsibility:** Controllers devem coordenar requisições, sem acumular regras complexas. Validações extensas podem ir para Form Requests, mantendo os métodos enxutos e dentro do limite de 20 linhas da atividade.
10. **`route:list`:** Lista métodos HTTP, URLs, nomes e controllers das rotas. Ajuda a equipe a documentar, conferir e auditar os endpoints disponíveis.

---

## 2. Checklist de Qualidade

- [x] **1. Verbos HTTP semânticos:** As ações de alteração e exclusão usam `PATCH`, `PUT` ou `DELETE`; `GET` é usado apenas para consultar dados.
- [x] **2. Resource Controller:** O `ClienteController` foi criado com o comando `php artisan make:controller ClienteController --resource`, gerando as sete ações CRUD.
- [x] **3. Proteção CSRF:** Todos os formulários `POST`, `PUT`, `PATCH` e `DELETE` contêm a diretiva `@csrf`.
- [x] **4. Method Spoofing:** Os formulários de edição e exclusão usam `@method('PUT')` ou `@method('DELETE')`, pois formulários HTML não enviam esses verbos nativamente.
- [x] **5. Rotas nomeadas:** Os links e formulários utilizam o helper `route('nome.da.rota')`, evitando URLs fixas escritas manualmente.
- [x] **6. Injeção de dependência:** Os métodos `store()` e `update()` recebem `Request $request` automaticamente pelo Service Container do Laravel.
- [x] **7. Restrições de rota:** Os parâmetros dinâmicos usam `whereNumber()` ou `whereAlphaNumeric()` para validar o formato antes de chegar ao controller.
- [x] **8. Métodos curtos:** Cada método possui no máximo 20 linhas e mantém uma única responsabilidade.
- [x] **9. Modo estrito:** Todos os arquivos PHP iniciam com `declare(strict_types=1);`.
- [x] **10. Documentação em português:** Comentários, mensagens e nomes de variáveis estão escritos em português do Brasil.
- [x] **11. Auditoria e Validação:** As rotas foram auditadas via `php artisan route:list` para garantir a integridade de todos os endpoints.