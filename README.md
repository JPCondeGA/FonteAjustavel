# Fonte Ajustável

## Introdução
 Projeto realizado para a disciplina de Eletrônica para Computação no ICMC, USP São Carlos. O projeto consiste na contrução de um fonte de tensão ajustável, que converte corrente alternada para contínua. A corrente alternada provém da rede elétrica com tensão RMS 127 volts (frequência da corrente 60Hz) e a tensão da corrente contínua resultante deve ser possível de ser ajustada nos valores entre 12 e 3 volts, entregando 100 mA quando está em 12 V e a carga da fonte possuir 120 ohm.  

## Explicação dos Componentes e do Projeto

### Transformador
 Componente capaz de aumentar ou diminuir a tensão em um circuito. No nosso caso, será usado para diminuir a tensão que vêm da tomada para a fonte poder usá-la. A tensão RMS (tensão efetiva se usada em um circuito de CA) que vêm da rede elétrica é 127 volts e 60 Hz de frequência. Para se calcular a RMS, é feita a integral da senóide da onda descrita pela corrente (pico da senoide dividido por √2). Portanto, para sabermos o pico dessa tensão, fazemos 127/√2 = 179,6 V, isto é, 179,6 volts é o pico da tensão que vem da tomada. 
  
  Voltando ao transformador, ele é constituído por duas bobinas com quantidade de voltas diferentes enroladas em um material ferromagnético (como no desenho abaixo). 

  ![image](https://github.com/user-attachments/assets/3f5da713-2272-4da9-a45f-e38761a37ec6)
 
  Fonte: _https://manutencaodecabine.com.br/transformador-de-forca/_
  
  Seu funcionamento se baseia na relação entre o campo magnético gerado por uma das bobinas com a outra bobina que gera uma tensão induzida. O núcleo ferromagnético ajuda essa interação acontecer, conduzindo o campo. Assim, a diminuição da tensão ocorre a depender da relação entre voltas dos enrolamentos: enrolamento primária com maior número de espiras é ligado a rede elétrica, enrolamento secundário com menor número de voltas é conectado à fonte. O transformador escolhido disponibilizado pelo professor foi aquele cuja tensão medida no capacitor era de 22 V. Testando no simulador, chegamos que o transformador tem uma razão entre o número de voltas igual a 7,45. Dessa forma, o pico da tensão que sai do transformador (pois a corrente ainda é alternada) conectado na tensão da tomada é 179,6/7,45 ~ 24,1 V (pico da tensão antes da ponte de diodo).
 
  É importante notar ainda que a potência (P = U * I) é igual nos dois lados do transformador, assim como no enrolamento primário tem uma tensão maior, a corrente nele é menor e por isso, apresenta fios mais finos. Então, os fios menores servem para ligar na tomada! (muito importante para não explodir o transformador).

### Ponte de Diodo
  Componente formado por quatro diodos e possui a finalidade de transformar os vales da onda em picos, processo que denominamos como retificação da onda. Graças a esse elemento, aproveitamos ao máximo a onda de corrente alternada no circuito, transformando o que chamamos de meia onda em onda completa. 
  
  Nele, os diodos, componentes que permitem a passagem de corrente somente em uma direção (anodo para o catodo), são organizados de forma que na parte positiva e na parte negativa da onda sempre a corrente passe por dois diodos e é impedida por outros dois e entregue para o circuito sempre o positivo para o mesmo lado do circuito e o negativo para o outro lado. Como cada diodo precisa de 0,7 V para começar a conduzir e sempre a corrente passa por dois (um na ida e outro na volta), a tensão que será passada no restante circuito será 24,1 - 2*0,7 = 24,1 - 1,4 = 22,7 V. O seguinte diagrama representa a ponte de diodo, veja que o positivo sempre sai para o mesmo lado e o negativo para o lado oposto:
  
  ![image](https://github.com/user-attachments/assets/2e1e0331-2af5-4a96-b49d-f1c2d8fbf2dd)
  
  Fonte: _https://celista.com.br/ponte-retificadora-o-que-e-como-testar/_ 

 A onda resultante é do tipo:
 
 ![image](https://github.com/user-attachments/assets/b41d7d64-635e-41c9-b79f-c0545d47e3a5)
 
 Fonte: _https://www.cmm.gov.mo/por/exhibition/secondfloor/moreinfo/2_16_0_DiodeLab.html_
 

 Assim, a quantidade de picos aumentou, ou seja, a frequência aumentou, ou melhor, dobrou. Então, a frequência é 60 * 2 = 120 Hz.

### Capacitor
 Componente capaz de armazenar carga. No nosso circuito, foi utilizado para diminuir o ripple da corrente, isto é, a diferença entre a tensão mínima e máxima da onda, que nesse ponto do circuito é o próprio 22,7 V. (22,7 - 0). O capacitor ficará sendo carregado, quando a corrente está no pico (e isso não impede que a corrente vá para o restante do circuito, ela só divide), e, quando ela começar a abaixar, haverá uma diferença de potencial entre o capacitor (que terá aproximadamente o potencial do pico) e o restante do circuito. Consequentemente, ele começará a descarregar, mantendo a tensão do circuito alta. 
 
 Além disso, é importante lembrar que o tempo de carregamento e descarregamento é proporcional à capacitância (o quanto o capacitor é bom em armazenar carga dada uma tensão) e a resistência presente no circuito. Quanto maior esse tempo melhor para nosso caso, pois assim o circuito será alimentado por mais tempo pelo capacitor, ou seja, o mínimo da onda será maior, assim o ripple (a diferença) será menor. Dessa forma, quanto maior a capacitância do nosso capacitor, menor ripple e melhor fica a situação da onda para o restante do circuito. 

### Diodo Zener
 Componente que funciona como um diodo se colocado da maneira convencional no circuito, porém se colocado ao contrário (modo zener) faz com que só passe corrente por ele a partir de um valor específico de diferença de potencial. Assim, utilizamos o diodo zener no modo zener para travar a tensão nos componentes paralelos a ele em 13 V (já que queremos uma fonte que entrega no máximo 12 V). Qualquer excesso de tensão acima de 13 V originário do ripple passará pelo zener. Assim, dizemos que esse diodo zener possui tensão zener de 13 V. Isso, junto do capacitor, estabiliza quase que totalmente a corrente, originando praticamente uma corrente contínua. 
 
 É importante dizer que o zener aguenta pouca potência, por volta de 400 mW, porém também precisa de uma corrente mínima para ligar. Assim, o resistor antes dele deve ser muito bem escolhido.
 
### Potenciômetro
 Componente que bifurca a corrente em dois caminhos, com um deles tendo resistência ajustável. No nosso circuito é usado para ajustar a tensão entre a base e o emissor do transistor com a resistência ajustável, mudando assim a tensão no dispositivo que será conectado como carga da fonte.

### Transistor
  Componente que ao ter corrente na base, permite a passagem de corrente entre coletor e emissor. No nosso circuito, ele é muito importante para que a tensão na carga seja a que está sendo estabilizada pelo zener diminuída ou não pelo potenciômetro, e, ao mesmo tempo, a corrente que passa pela carga seja maior que a oferecida pelo potenciômetro. A tensão no emissor de um transistor pode ser calculada por meio da subtração entre a tensão entre a base e o emissor (a qual é aquela oferecida pelo potenciômetro)  e a tensão necessária para ligar o transistor (cerca de 0,7 V). Caso o potenciômetro esteja no mínimo de resistência, então: 13 - 0,7 = 12,3 V
 
  Ou seja, a tensão na carga será 12,3 V com o potenciômetro no mínimo, sendo possível a carga pegar 12 V, como desejado. Já a corrente que passa pela carga pode ser dada pela corrente que vai até a base multiplicada pelo fator de amplificação de corrente do transistor, que normalmente é 100. Assim, a corrente que vai até a base deve ser no mínimo 1 mA, para que na carga seja 1 * 100 = 100 mA, cumprindo os requisitos do projeto.

### Resistores
 Componentes capazes de segurar uma parte da tensão do circuito. No nosso circuito, foi utilizado para limitar a corrente e a potência que passam pelos componentes, a fim de não permitir a queima deles e, simultaneamente, permitir que continuem ligados. Seguindo os valores da imagem do simulador Falstad, temos:
* R1 (de 2.2k Omhs no Falstad): diminui a corrente que passa pelo LED, evitando que esse queime, e também não “roubando” as correntes dos circuitos em paralelo.
* R2 (de 510 Omhs no Falstad): controla a corrente que passa pelo zener, deve ter o valor alto suficiente para que o mínimo de corrente passe pelo zener, já que essa corrente é um desperdício para a finalidade do circuito e pode queimar o zener; mas não pode ser alto a ponto de não passar a corrente mínima no zener, desligando-o.
* R3 (de 2k Omhs no Falstad, logo abaixo ao pontenciômetro): utilizado para que tensão seja dividida entre o potenciômetro e ele; assim, mesmo que o potênciometro esteja no máximo de resistência, o caminho que vai para a base do transistor não terá 0 V, mas sim a tensão segurada pelo R3; ou seja, se quisermos alterar a tensão mínima oferecida pela fonte, alteramos o R3. 
* R4 (de 45 Omhs no Falstad): diminui a potência que passa pelo transistor para que este não queima; ele aguenta aproximadamente 1 W, porém quando o potenciômetro está no máximo de resistência, a potência no transistor tende a aumentar muito, já que com maior resistência nesse ramo em paralelo, irá passar menor corrente por ele e maior pelo transistor.
* R5 (de 120 Omhs no Falstad): representa o celular ou outro dispositivo que esteja sendo alimentado pelo circuito.

## Cálculo da Capacitância
 A capacitância escolhida para o capacitor pode ser calculada usando a seguinte fórmula: 
 
 Para aplicarmos ela, devemos saber o valor da corrente total do circuito, tensão de ripple (que varia) e a frequência da onda. Já sabemos a frequência (120 Hz) e, sendo o ripple buscado de no mínimo 10% (considerado ideal para esse tipo de fontes), então Vripple = 0,1 * 22,7 = 2,2 V (assim a onda está indo de 22,7 V até  20,5 V). Desse modo, falta sabermos a corrente total que passa pelo circuito. Para isso, somamos a corrente que passa por cada ramo paralelo. 
 
 No LED, desejamos uma corrente de 10 mA, já que 20 mA tem perigo de queimá-lo. Com isso que chegamos no valor do R1, pois (V é a tensão pico (caso mais crítico) após a ponte de diodo e Vled a tensão usada para ligar o LED): 
 
    Iled = V/R => Iled = (V - Vled) / R1 => 10^(-2) = (22,5 - 2,8) / R1 => R1 = 1870 K

 OBS: utilizamos de 2K, que só diminuirá mais um pouco a corrente, sem prejuízo para a utilização do LED.
 
 Na carga, chegará a uma corrente que depende da tensão que o zener bloqueia (Vzener), oferecendo para o circuito em paralelo, a tensão necessária para ligar o transistor (Vbe) e do coeficiente beta (B) do transistor (coeficiente de aumento de corrente que no nosso caso é 100), além da resistência da carga. Assim: 
  
    * Icarga = ((Vzener - Vbe) / Rcarga) * B = ((13 - 0,7) / 120) * 100 ~ 0,1 A = 100 mA (valor que queríamos).
 
  Já no ramo do potenciômetro, teremos que ver o valor total dos resistores nessa trajetório:
  
    Rt = 600 + 5000 + 2000 = 7600 Ohms
    
  Assim:
  
    Ipot = 22,7 / 7600 ~ 0,003 = 3 mA
    
  Por fim, a corrente que passa pelo zener devemos calcular levando em consideração que o zener bloqueia 13 V, assim somente a os valores acima desse farão corrente passar por ele. Além disso, precisamos lembrar que R2 está em série com, ficando:
    
    Izener = (22,7 - 13)/600 ~ 0,016 = 16 mA 
  
  Portanto, sendo a corrente total a soma de todas em paralelo, conseguimos:
    
    I = Iled + Icarga + Ipot + Izener = 0,01 + 0,1 + 0,003 + 0,016 = 0,128 = 129 mA
   
  Agora sim obtemos todos os "ingredientes" para calcular a capacitância:
    
    C = I / (f * Vripple) = 0,129 / (120 * 2,2) ~ 0,000488 = 488 uF
   
   OBS: o capacitor utilizado no projeto real foi o de 680 uF, porém isso não afeta negativamente o projeto, pois como já explicado, quanto maior a capacitância, menor o ripple, o que faz a onda ficar ainda mais estável.

## Tabela de Preços

| Componente | Quantidade | Valor |
|---------|------------|-------|
|Transformador 15+15VAC| 1 | R$ 38,60|
|Ponte retificadora | 1 | R$ 3,90|
|Capacitor 680 uF | 1 | R$ 5,80|
|Diodo Zener 13V| 1 | R$ 0,50|
|Potenciômetro 5K| 1 | R$ 7,00|
|LED| 1 | R$ 0,50| 
|Resistor 100R 2W| 1 | R$ 1,20|
|Resistor 82R 2W| 1 | R$ 1,20|
|Resistor 120R 2W| 1 | R$ 1,20|
|Resistor 1000R | 1 | R$ 0,07 * 2 = R$ 0,14|
|Resistor 2.2R | 1 | R$ 0,07|
|Resistor 510R | 1 | R$ 0,07| 
|Protoboard 2 Barras| 1 | R$ 39,10

OBS1: perceba que usamos 510 Ohms ao em vez de 600 Ohms no R2, o que aumentou um pouco a corrente sobre o zener, mas sem prejudicar o circuito.

OBS2: perceba também que não há o resistor de 2000 Ohms e o de 45 Ohms, porém esses foram feitos colocando dois de 1000 Ohms em sére e colocando um de 100 e outro 82 em paralelo, respectivamente.

OBS3: protoboard é uma placa utilizada para prototipação de circuitos, ou seja, onde se conecta os demais componentes; por ela não fazer parte do circuito em si, não foi explicada nos tópicos superiores.

## Projeto no Simulador Falstad

![image](https://github.com/user-attachments/assets/0a3dda83-dcf1-4a67-8da2-92751b13621f)

Link: https://tinyurl.com/2ygrcmyx

## Projeto no EAGLE 

### Esquemático

![esquemático](https://github.com/user-attachments/assets/cc143ecd-f127-4374-a5b3-3062d4c9595b)

### Layout da PCB

![layout](https://github.com/user-attachments/assets/b754c4dd-0ce6-42c6-a7e8-353d21c39b4d)

## Fotos do Projeto

![image](https://github.com/user-attachments/assets/7487e3f3-a520-4b81-8a58-1dc3e23a68e5)

![image](https://github.com/user-attachments/assets/d746fa91-73ab-4080-9802-59c948d7c0f4)

## Vídeo Explicativo

Link: https://youtu.be/EH_kWGaPv54

## Grupo

* João Pedro Conde Gomes Alves
* Antonio Carlos Madalozzo Gonzaga
* Danilo de Oliveira Lopes
* Eduardo Benedini Bueno

