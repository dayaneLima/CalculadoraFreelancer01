# CalculadoraFreelancer01

Se trata de um app inicial para cálculo do valor da hora do profissional freelancer.

## Como criar um projeto Xamarin Forms no Visual Studio

Para criar um projeto Xamarin Forms vá em  <i>File -> new -> Project</i>

Em Visual C#, escolha a opção  <i>Cross-platform</i>, a direita terá somente a opção <i>Mobile App(Xamarin Forms)</i>, a escolha e dê um nome para o projeto. Clique em Ok.

Agora escolha a opção <i>Blank App</i>. Deixe marcado as opções IOS e Android. Marque a opção <i>.NET Standard</i> e clique em OK. O projeto será criado.

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

Ao criarmos um projeto em Xamarin Forms nem sempre ele vem atualizado com a última versão do framework. Então antes de começar a codificarmos é bom atualizar para a última versão das bibliotecas do Xamarin Forms. 

Para isso clique com o botão direito sobre a solution e vá em <i>Manage Nuget Packages for Solution</i>. Na guia aberta, escolha <i>Updates</i>, marque todas e clique em <i>install</i>.

![Atualização via Nuget](https://github.com/dayaneLima/CalculadoraFreelancer01/blob/master/Docs/Gifs/atualizacaoNuget.gif)

## Tela de cálculo do valor da hora

Vamos criar uma Page chamada CalculoValorHoraPage, clique com o botão direito sobre o projeto principal (chamado CalculadoraFreelancer01), vá em <i>Add -> new item</i>, escolha Xamarin Forms, nas opções a esquerda que serão mostradas, escolha a escrita <i>Content Page</i>. Cuidado para não escolher a <i>Content Page (C#)</i>. Esta última criará somente a classe em c#, não tendo o arquivo .xaml para criação de layouts com xml.

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
            
            <Label Text="Valor ganho por mês" />
            <Entry Placeholder="Valor ganho por mês"
                   x:Name="ValorGanhoMes"
                   Keyboard="Numeric"/>

            <Label Text="Valor ganho por mês" />
            <Entry Placeholder="Horas trabalhadas por dia"
                   x:Name="HorasTrabalhadasPorDia"
                   Keyboard="Numeric"/>

            <Label Text="Dias trabalhados por mês" />
            <Entry Placeholder="Dias trabalhados por mês"
                   x:Name="DiasTrabalhadosPorMes"
                   Keyboard="Numeric"/>

            <Label Text="Dias de férias por ano" />
            <Entry Placeholder="Dias de férias por ano"
                   x:Name="DiasFeriasPorAno"
                   Keyboard="Numeric"/>

            <Label Text="R$ 00,00 / hora"
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

<img src="https://github.com/dayaneLima/CalculadoraFreelancer01/blob/master/Docs/Imgs/calculadoraFreelancerO1TelaValorHora.PNG" alt="Tela calculadora freelancer" width="260">

Utilizamos nos campos de entrada de texto (Entry) o Keyboard="Numeric", mas há outros tipos de teclado, como Email e Telephone. Pra mais informações veja a documentação da Microsoft: <a  href='https://docs.microsoft.com/en-us/xamarin/xamarin-forms/user-interface/text/entry' target="_blank">Documentação do Entry</a>

## Cálculo do valor da hora

Todo arquivo .xaml tem uma classe vinculada a ele, terminado com o nome .xaml.cs, como mostrado na imagem abaixo.


Tudo que é feito no xaml, conseguimos acessar na nossa classe C#, e nessa classe também conseguimos criar layouts e atribuir no nosso xaml. Ao utilizarmos essa classe, falamos que estamos fazendo código em <i>CodeBehind</i>.

Então vamos no arquivo CalculoValorHoraPage.xaml.cs, no construtor da classe vamos atribuir o evento de click para o nosso botão de calcular. O código ficará como o mostrado abaixo:

```c#
	public CalculoValorHoraPage ()
		{
          InitializeComponent ();
          CalcularValorHoraButton.Clicked += CalcularValorHoraButton_Clicked;
		}
````

Agora criaremos a função responsável pelo cálculo:

```c#
     private void CalcularValorHoraButton_Clicked(object sender, EventArgs e)
        {

            double valorGanhoAnual = double.Parse(ValorGanhoMes.Text) * 12;
            int totalDiasTrabalhadosPorAno = int.Parse(DiasTrabalhadosPorMes.Text) * 12;

            if (!string.IsNullOrEmpty(DiasFeriasPorAno.Text))
            {
                totalDiasTrabalhadosPorAno -= int.Parse(DiasFeriasPorAno.Text);
            }

            double valorHora = valorGanhoAnual / (totalDiasTrabalhadosPorAno * int.Parse(HorasTrabalhadasPorDia.Text));

            ValorDaHora.Text = $"{valorHora.ToString("C")} / hora";

        }
````
 
## Resultado

Vamos mandar executar o projeto e testar o cálculo:

<img src="https://github.com/dayaneLima/CalculadoraFreelancer01/blob/master/Docs/Gifs/calculadoraFreelancer01.gif" alt="Tela App Calculadora Freelancer funcionando" width="260">
