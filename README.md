# ⛽ Calculadora de Combustível em .NET MAUI

**Atividade da Agenda 10 — Desenvolvimento de Sistemas II (DS2)**  
*Centro Paula Souza - ETEC Deputado Ary de Camargo Pedroso*  
**Aluno:** Donizete dos Santos  
**Professor Mediador:** Tadeu Fernando Piran  

---

## 📌 Descrição do Projeto
Aplicativo móvel multiplataforma desenvolvido em **.NET MAUI (C# e XAML)** para cálculo comparativo de rendimento entre Etanol e Gasolina. O projeto foi expandido para incluir a validação de dados com identificação do veículo (Marca e Modelo) e exibição do resultado de forma personalizada via alertas modais (`DisplayAlert`).

---

## 🛠️ Tecnologias Utilizadas
* **Plataforma:** .NET 8.0 MAUI
* **Linguagens:** C# e XAML
* **Ambiente de Desenvolvimento:** Visual Studio 2022
* **Layout:** `VerticalStackLayout` e `ScrollView`

---

## 🚀 Funcionalidades Implementadas
- [x] Entradas de texto para **Marca do Veículo** e **Modelo do Veículo** (`txt_marca` e `txt_modelo`);
- [x] Entradas de valores numéricos para o preço do **Etanol** e da **Gasolina** (`txt_etanol` e `txt_gasolina`);
- [x] Validação de campos vazios e tratamento de exceções com estrutura `try-catch`;
- [x] Lógica de decisão baseada na regra de 70% ($Etanol \le Gasolina \times 0.7$);
- [x] Exibição de alerta interativo personalizado com a indicação do combustível ideal para o veículo informado.

---

## 📹 Vídeo de Demonstração
> 🔗 **Assista à demonstração do projeto funcionando:**  
> [Cole aqui o link do seu vídeo do YouTube ou Google Drive/OneDrive]

---

## 📂 Estrutura Principal do Código

### `MainPage.xaml` (Interface Gráfica)
```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage x:Class="MauiAppMeuCombustivel.MainPage" xmlns="[http://schemas.microsoft.com/dotnet/2021/maui](http://schemas.microsoft.com/dotnet/2021/maui)" xmlns:x="[http://schemas.microsoft.com/winfx/2009/xaml](http://schemas.microsoft.com/winfx/2009/xaml)">

    <ScrollView>
        <VerticalStackLayout Padding="30,0" Spacing="15">

            <Image Aspect="AspectFit" HeightRequest="185" SemanticProperties.Description="dot net bot in a race car number eight" Source="dotnet_bot.png"/>

            <!-- Entrada de dados do Veículo -->
            <Label Text="Marca do Veículo:"/>
            <Entry Placeholder="Ex: Fiat, Chevrolet" x:Name="txt_marca"/>

            <Label Text="Modelo do Veículo:"/>
            <Entry Placeholder="Ex: Uno, Onix" x:Name="txt_modelo"/>

            <!-- Preços dos combustíveis -->
            <Label Text="Preço do Etanol:"/>
            <Entry Keyboard="Numeric" Placeholder="R$ 0,00" x:Name="txt_etanol"/>

            <Label Text="Preço da Gasolina:"/>
            <Entry Keyboard="Numeric" Placeholder="R$ 0,00" x:Name="txt_gasolina"/>

            <!-- Botão de Processamento -->
            <Button Clicked="Button_Clicked" Margin="0,10,0,0" Text="Qual compensa mais?"/>

        </VerticalStackLayout>
    </ScrollView>

</ContentPage>
using System;

namespace MauiAppMeuCombustivel
{
    public partial class MainPage : ContentPage
    {
        public MainPage()
        {
            InitializeComponent();
        }

        private void Button_Clicked(object sender, EventArgs e)
        {
            try
            {
                string marca = txt_marca.Text?.Trim();
                string modelo = txt_modelo.Text?.Trim();

                if (string.IsNullOrEmpty(marca) || string.IsNullOrEmpty(modelo))
                {
                    DisplayAlert("Atenção", "Por favor, informe a marca e o modelo do veículo.", "OK");
                    return;
                }

                double etanol = Convert.ToDouble(txt_etanol.Text);
                double gasolina = Convert.ToDouble(txt_gasolina.Text);

                string msg = "";

                if (etanol <= (gasolina * 0.7))
                {
                    msg = $"O etanol está compensando para o seu {marca} {modelo}.";
                }
                else
                {
                    msg = $"A gasolina está compensando para o seu {marca} {modelo}.";
                }

                DisplayAlert("Calculado", msg, "OK");
            }
            catch (Exception ex)
            {
                DisplayAlert("Ops", "Insira valores válidos nos campos: " + ex.Message, "Fechar");
            }
        }
    }
}

