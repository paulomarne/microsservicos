Arquitetura de exemplo de microsservi�os usando ASP.NET Core, Ocelot, MongoDB e JWT.

# Ambiente de desenvolvimento

- Visual Studio 2022 >= 17.8.0
- .NET 8.0
- MongoDB
- Postman

# Arquitetura

Existem tr�s microservi�os:

- **CatalogMicroservice**: permite gerir o cat�logo.
- **CartMicroservice**: permite gerir o carrinho.
- **IdentityMicroservice**: permite gerir os utilizadores.

Cada microsservi�o implementa uma �nica capacidade de neg�cio e tem a sua pr�pria base de dados MongoDB.

Existem dois gateways de API, um para o frontend e outro para o backend.

Abaixo est� o gateway de API do frontend:

- **GET /catalog**: recupera itens do cat�logo.
- **GET /catalog/{id}**: recupera um item do cat�logo.
- **GET /cart**: recupera itens do carrinho.
- **POST /cart**: adiciona um item do carrinho.
- **PUT /cart**: actualiza um item do carrinho.
- **DELETE /cart**: elimina um item do carrinho.
- **POST /identity/login**: efectua um in�cio de sess�o.
- **POST /identity/register**: regista um utilizador.
- **GET /identity/validate**: valida um token JWT.

Abaixo est� o gateway da API backend:

- **GET /catalog**: recupera itens do cat�logo.
- **GET /catalog/{id}**: recupera um item do cat�logo.
- **POST /catalog**: cria um item de cat�logo.
- **PUT /catalog**: actualiza um item do cat�logo.
- **DELETE /catalog**: elimina um item do cat�logo.
- **PUT /cart/update-catalog-item**: actualiza um item de cat�logo nos carrinhos.
- **DELETE /cart/delete-catalog-item**: elimina refer�ncias de itens de cat�logo dos carrinhos.
- **POST /identity/login**: efectua um in�cio de sess�o.
- **POST /identity/register**: regista um utilizador.
- **GET /identity/validate**: valida um token JWT.

Finalmente, existem duas aplica��es cliente. Um frontend para aceder � loja e um backend para gerir a loja.

O frontend permite que os utilizadores registados vejam os itens de cat�logo dispon�veis, adicionem itens de cat�logo ao carrinho e removam itens de cat�logo do carrinho.

O backend permite que os utilizadores administrativos vejam os itens de cat�logo dispon�veis, adicionem novos itens de cat�logo e removam itens de cat�logo.

# C�digo fonte

- O projeto **CatalogMicroservice** cont�m o c�digo-fonte do microsservi�o que gerencia o cat�logo.
- O projeto **CartMicroservice** cont�m o c�digo fonte do microservi�o que gere o carrinho.
- O projeto IdentityMicroservice** cont�m o c�digo fonte do microsservi�o de gest�o dos utilizadores.
- O projeto **Middleware** cont�m o c�digo-fonte das funcionalidades comuns utilizadas pelos microsservi�os.
- O projeto FrontendGateway** cont�m o c�digo fonte do gateway da API de frontend.
- O projeto BackendGateway** cont�m o c�digo-fonte do gateway da API de backend.
- O projeto **Frontend** cont�m o c�digo fonte da aplica��o cliente frontend.
- O projeto **Backend** cont�m o c�digo fonte da aplica��o cliente de backend.

# Como executar a aplica��o

Voc� pode executar o aplicativo usando o IISExpress no Visual Studio 2022 ou no Docker.

Ser� necess�rio instalar o MongoDB se ele n�o estiver instalado.

Primeiro, clique com o bot�o direito do mouse na solu��o, clique em propriedades e selecione v�rios projetos de inicializa��o. Selecione todos os projetos como projetos de inicializa��o, exceto Middleware, Modelo e projetos de testes de unidade.

Em seguida, pressione **F5** para executar o aplicativo.

Pode aceder ao frontend a partir de https://localhost:44317/.

Pode aceder ao backend a partir de https://localhost:44301/.

Para iniciar sess�o no frontend pela primeira vez, basta clicar em **Registar** para criar um novo utilizador e iniciar sess�o.

Para iniciar sess�o no backend pela primeira vez, ter� de criar um utilizador administrador. Para isso, abra o Swagger em https://localhost:44397/ ou Postman e execute o seguinte pedido POST https://localhost:44397/api/identity/register com o seguinte payload:

```js
{
  �email": �admin@store.com�,
  �password": �password�,
  �isAdmin": verdadeiro
}
```
Finalmente, pode iniciar sess�o no backend com o utilizador admin que criou e criar novos produtos.

Se quiser modificar a string de conex�o do MongoDB, � necess�rio atualizar o *appsettings.json* dos microsservi�os e gateways.

# Referncias

- Estilo de arquitetura de microsservi�os](https://docs.microsoft.com/en-us/azure/architecture/guide/architecture-styles/microservices)
- [Monitoramento de integridade](https://docs.microsoft.com/en-us/dotnet/architecture/microservices/implement-resilient-applications/monitor-app-health)
- [Balanceamento de carga](https://ocelot.readthedocs.io/en/latest/features/loadbalancer.html)
- [Testando servi�os ASP.NET Core](https://docs.microsoft.com/en-us/dotnet/architecture/microservices/multi-container-microservice-net-applications/test-aspnet-core-services-web-apps)
