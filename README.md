Arquitetura de exemplo de microsserviços usando ASP.NET Core, Ocelot, MongoDB e JWT.

# Ambiente de desenvolvimento

- Visual Studio 2022 >= 17.8.0
- .NET 8.0
- MongoDB
- Postman

# Arquitetura

Existem três microserviços:

- **CatalogMicroservice**: permite gerir o catálogo.
- **CartMicroservice**: permite gerir o carrinho.
- **IdentityMicroservice**: permite gerir os utilizadores.

Cada microsserviço implementa uma única capacidade de negócio e tem a sua própria base de dados MongoDB.

Existem dois gateways de API, um para o frontend e outro para o backend.

Abaixo está o gateway de API do frontend:

- **GET /catalog**: recupera itens do catálogo.
- **GET /catalog/{id}**: recupera um item do catálogo.
- **GET /cart**: recupera itens do carrinho.
- **POST /cart**: adiciona um item do carrinho.
- **PUT /cart**: actualiza um item do carrinho.
- **DELETE /cart**: elimina um item do carrinho.
- **POST /identity/login**: efectua um início de sessão.
- **POST /identity/register**: regista um utilizador.
- **GET /identity/validate**: valida um token JWT.

Abaixo está o gateway da API backend:

- **GET /catalog**: recupera itens do catálogo.
- **GET /catalog/{id}**: recupera um item do catálogo.
- **POST /catalog**: cria um item de catálogo.
- **PUT /catalog**: actualiza um item do catálogo.
- **DELETE /catalog**: elimina um item do catálogo.
- **PUT /cart/update-catalog-item**: actualiza um item de catálogo nos carrinhos.
- **DELETE /cart/delete-catalog-item**: elimina referências de itens de catálogo dos carrinhos.
- **POST /identity/login**: efectua um início de sessão.
- **POST /identity/register**: regista um utilizador.
- **GET /identity/validate**: valida um token JWT.

Finalmente, existem duas aplicações cliente. Um frontend para aceder à loja e um backend para gerir a loja.

O frontend permite que os utilizadores registados vejam os itens de catálogo disponíveis, adicionem itens de catálogo ao carrinho e removam itens de catálogo do carrinho.

O backend permite que os utilizadores administrativos vejam os itens de catálogo disponíveis, adicionem novos itens de catálogo e removam itens de catálogo.

# Código fonte

- O projeto **CatalogMicroservice** contém o código-fonte do microsserviço que gerencia o catálogo.
- O projeto **CartMicroservice** contém o código fonte do microserviço que gere o carrinho.
- O projeto IdentityMicroservice** contém o código fonte do microsserviço de gestão dos utilizadores.
- O projeto **Middleware** contém o código-fonte das funcionalidades comuns utilizadas pelos microsserviços.
- O projeto FrontendGateway** contém o código fonte do gateway da API de frontend.
- O projeto BackendGateway** contém o código-fonte do gateway da API de backend.
- O projeto **Frontend** contém o código fonte da aplicação cliente frontend.
- O projeto **Backend** contém o código fonte da aplicação cliente de backend.

# Como executar a aplicação

Você pode executar o aplicativo usando o IISExpress no Visual Studio 2022 ou no Docker.

Será necessário instalar o MongoDB se ele não estiver instalado.

Primeiro, clique com o botão direito do mouse na solução, clique em propriedades e selecione vários projetos de inicialização. Selecione todos os projetos como projetos de inicialização, exceto Middleware, Modelo e projetos de testes de unidade.

Em seguida, pressione **F5** para executar o aplicativo.

Pode aceder ao frontend a partir de https://localhost:44317/.

Pode aceder ao backend a partir de https://localhost:44301/.

Para iniciar sessão no frontend pela primeira vez, basta clicar em **Registar** para criar um novo utilizador e iniciar sessão.

Para iniciar sessão no backend pela primeira vez, terá de criar um utilizador administrador. Para isso, abra o Swagger em https://localhost:44397/ ou Postman e execute o seguinte pedido POST https://localhost:44397/api/identity/register com o seguinte payload:

```js
{
  “email": “admin@store.com”,
  “password": “password”,
  “isAdmin": verdadeiro
}
```
Finalmente, pode iniciar sessão no backend com o utilizador admin que criou e criar novos produtos.

Se quiser modificar a string de conexão do MongoDB, é necessário atualizar o *appsettings.json* dos microsserviços e gateways.

# Referncias

- Estilo de arquitetura de microsserviços](https://docs.microsoft.com/en-us/azure/architecture/guide/architecture-styles/microservices)
- [Monitoramento de integridade](https://docs.microsoft.com/en-us/dotnet/architecture/microservices/implement-resilient-applications/monitor-app-health)
- [Balanceamento de carga](https://ocelot.readthedocs.io/en/latest/features/loadbalancer.html)
- [Testando serviços ASP.NET Core](https://docs.microsoft.com/en-us/dotnet/architecture/microservices/multi-container-microservice-net-applications/test-aspnet-core-services-web-apps)
