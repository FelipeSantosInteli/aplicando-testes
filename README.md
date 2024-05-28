# Aplicando testes

O código se trata de um conversor de temperatura de Fahrenheit para Celsius e testes unitários para verificar a precisão do conversor, escritos em três frameworks de teste diferentes: o xUnit, NUnit e o MSTest.

```
using System;

namespace Temperatura
{
    public static class ConversorTemperatura
    {
        public static double FahrenheitParaCelsius(double temperatura)
            //=> (temperatura - 32) / 1.8; // Simulação de falha
            => Math.Round((temperatura - 32) / 1.8, 2);
    }
}
```

## Testes

### xUnit

xUnit é um framework de teste para .NET que permite escrever testes unitários utilizando o atributo `[Theory]` junto com `[InlineData]` para fornecer dados de entrada diretamente nos testes.

Para cada par de valores (Fahrenheit, Celsius), o método `FahrenheitParaCelsius` é chamado e o resultado é comparado com o valor esperado.

```
using System;
using Xunit;

namespace Temperatura.Testes
{
    public class TestesConversorTemperatura
    {
        [Theory]
        [InlineData(32, 0)]
        [InlineData(47, 8.33)]
        public void TestarConversaoTemperatura(double fahrenheit, double celsius)
        {
            double valorCalculado = ConversorTemperatura.FahrenheitParaCelsius(fahrenheit);
            Assert.Equal(celsius, valorCalculado);
        }
    }
}
```
- 32°F para 0°C: [InlineData(32, 0)]
- 47°F para 8.33°C: [InlineData(47, 8.33)]

### NUnit

Um dos frameworks de teste mais antigos e mais utilizados para escrever testes unitários para .NET

Aqui é usado o atributo `[TestCase]` para fornecer conjuntos de dados de entrada e verificar a saída do método `FahrenheitParaCelsius`

```
using NUnit.Framework;

namespace Temperatura.Testes
{
    public class TestesConversorTemperatura
    {
        [TestCase(32, 0)]
        [TestCase(47, 8.33)]
        public void TesteConversaoTemperatura(double tempFahrenheit, double tempCelsius)
        {
            double valorCalculado = ConversorTemperatura.FahrenheitParaCelsius(tempFahrenheit);
            Assert.AreEqual(tempCelsius, valorCalculado);
        }
    }
}
```

- 32°F para 0°C: [TestCase(32, 0)]
- 47°F para 8.33°C: [TestCase(47, 8.33)]

### MSTest

Framework de teste fornecido pela Microsoft e integrado no Visual Studio.

Nele é utilizado o atributo `[DataTestMethod]` juntamente com `[DataRow]` para fornecer dados de teste diretamente no método

```
using Microsoft.VisualStudio.TestTools.UnitTesting;

namespace Temperatura.Testes
{
    [TestClass]
    public class TestesConversorTemperatura
    {
        [DataRow(32, 0)]
        [DataRow(47, 8.33)]
        [DataTestMethod]
        public void TesteConversaoTemperatura(double tempFahrenheit, double tempCelsius)
        {
            double valorCalculado = ConversorTemperatura.FahrenheitParaCelsius(tempFahrenheit);
            Assert.AreEqual(tempCelsius, valorCalculado);
        }
    }
}

```

- 32°F para 0°C: [DataRow(32, 0)]
- 47°F para 8.33°C: [DataRow(47, 8.33)]
