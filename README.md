# CalculadoraFreelancer01

Se trata de um app inicial para cálculo do valor da hora do profissional freelancer.

## Como criar um projeto Xamarin Forms no Visual Studio
![Criar Projeto Xamarin Forms](https://github.com/dayaneLima/CalculadoraFreelancer01/blob/master/Docs/Gifs/criacaoProjeto.gif)

## Navegação - App.xaml.cs
Como usaremos navegação entre telas, temos que definir que nossa tela inicial seja chamada já utilizando navegação. Abra o arquivo App.xaml.cs, no construtor tem o seguinte código:

```c#
  MainPage = new MainPage();
```

Altere para o cógido abaixo:

```c#
  MainPage = new NavigationPage(new MainPage());
```

## Verificar se está tudo certo
Execute o projeto e veja se abriu a tela default do xamarin, similar a imagem abaixo:

<img src="https://github.com/dayaneLima/CalculadoraFreelancer01/blob/master/Docs/Imgs/telaInicialXamarin.PNG" alt="Criar Página no Xamarin Forms" width="260">

## Atualização - Nuget

O Nuget é o gerenciador de pacotes para .NET. Através do Nuget você pode baixar bibliotecas de terceiros, além de poder criar as suas e compartilhá-las.

Ao criarmos um projeto em Xamarin Forms nem sempre ele vem atualizado com a última versão do framework. Então antes de começar a codificarmos é bom atualizar para a última versão das bibliotecas do Xamarin Forms. Abaixo mostra como gerenciar os pacotes via Nuget e atualizar as bibliotecas.

![Criar Página no Xamarin Forms](https://github.com/dayaneLima/CalculadoraFreelancer01/blob/master/Docs/Gifs/atualizacaoNuget.gif)

## Tela de cálculo do valor da hora

Vamos criar uma Page chamada CalculoValorHoraPage, abaixo é mostrado como criar uma página no Xamarin Forms:

![Criar Página no Xamarin Forms](https://github.com/dayaneLima/CalculadoraFreelancer01/blob/master/Docs/Gifs/criacaoPage.gif)

Esta tela será responsável por calcular o valor da hora do profissional freelancer. Precisaremos então para os cálculos saber qual é o valor que o profissional quer ganhar por mês, as horas trabalhadas por dia, quantos dias irá trabalhar por mês e por fim, quantos dias terá de férias por ano. Criaremos então um campo para cada item citado anteriormente. Precisaremos também de um campo para mostrar o resultado da operação, que é o valor da hora do profissional.

Edite o arquivo CalculoValorHoraPage.xaml e adicione o código abaixo:

 ```xml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="CalculadoraFreelancer01.CalculoValorHoraPage"
             Title="Valor da Hora"
             Padding="10">
    <ContentPage.Content>
        <StackLayout>
            
            <Entry Placeholder="Valor ganho por mês"
                   x:Name="ValorGanhoMes"/>
            
            <Entry Placeholder="Horas trabalhadas por dia"
                   x:Name="HorasTrabalhadasPorDia"/>
            
            <Entry Placeholder="Dias trabalhados por mês"
                   x:Name="DiasTrabalhadosPorMes"/>
            
            <Entry Placeholder="Dias de férias por ano"
                   x:Name="DiasFeriasPorAno"/>

            <Label Text="R$ 00,00"
                   x:Name="ValorDaHora"
                   FontSize="Large"
                   TextColor="Green"/>

            <Button Text="Calcular"
                    BackgroundColor="#6699ff"
                    TextColor="White"
                    x:Name="CalcularValorHoraButton"/>


        </StackLayout>
    </ContentPage.Content>
</ContentPage>
```` 

Agora mandamos executar o projeto, a tela gerada deverá ser igual a esta:

<img src="https://github.com/dayaneLima/CalculadoraFreelancer01/blob/master/Docs/Imgs/calculadoraFreelancerO1TelaValorHora.PNG" alt="Criar Página no Xamarin Forms" width="260">

