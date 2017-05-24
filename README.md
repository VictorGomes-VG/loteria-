# loteria-
?php
// feito por V .G 

function sorteado($gameEscolha , $quantosNumeros){
    $jogos = [1 => 60, 2 => 80, 3 => 100, 4 => 25];
    $numsSorteados = [0];
    $maximo = $jogos[$gameEscolha];
    for ($i = 0; $i < $quantosNumeros; $i++) {
        $sorteio = rand(1, $maximo);
        $count = count($numsSorteados);
        for ($j = 0; $j < $count; $j++) {
            if ($sorteio == $numsSorteados[$j]) {
                $sorteio = rand(1, 60);
                $j = 0;
            }
        }
        $numsSorteados[$i] = $sorteio;
    }

    sort($numsSorteados);

    foreach ($numsSorteados as $bagulhosos){
        echo "$bagulhosos\n";
    }

    return $numsSorteados;
}

function valor($gameEscolha, $quantosNumeros, $quantApostas){
    $precos = [
        "1"=> [6  => 3.5, 7 => 24.5, 8 => 98, 9 => 294, 10 => 735, 11 => 1617, 12 => 3234, 13 => 6006, 14 => 10510.50, 15 => 17517.50],
        "2"=> [5  => 1.5, 6 => 9, 7 => 31.5, 8 => 84, 9 => 189, 10 => 378, 11 => 693, 12 => 1188, 13 => 1930.5, 14 => 3003, 15 => 4504.5],
        "3"=> [50 => 1.5],
        "4"=> [15 => 2, 16 => 32, 17 => 272, 18 => 1632]
    ];

    return  $valor = $precos[$gameEscolha][$quantosNumeros] * $quantApostas;

}

$jogaveis =[ "1" => "Mega Sena", "2" => "Quina", "3" =>"lotomania", "4" =>"lotomania"];
$numeros = [
    "1"=> [6  , 7 , 8 , 9 , 10, 11 , 12 , 13 , 14 , 15 ],
    "2"=> [5 , 6 , 7 , 8 , 9 , 10 , 11 , 12 , 13 , 14 , 15 ],
    "3"=> [50],
    "4"=> [15, 16 , 17 , 18]
];

echo "escolha um jogo com um numero!!\n";

$gameEscolha = "";

do {
    echo "1-MegaSena \n";
    echo "2-Quina\n";
    echo "3-LotoMania\n";
    echo "4-LotoFacil\n";
    echo "5-sair\n";


    echo 'qual loteria tu vai querer?';
    $gameEscolha = trim(fgets(STDIN));

    if($gameEscolha < 1 or $gameEscolha > 5){
        echo "digite novamente, pois você digitou um cararcter inválido\n";
    }
}while($gameEscolha < 1 or $gameEscolha > 5);
if ($gameEscolha == 5 ){
    echo'volte sempre!';
    exit;
}

echo'quantas apostas tu deseja fazer meu rei ?';
$quantApostas =trim(fgets(STDIN));

echo "As dezenas permitidas para {$jogaveis[$gameEscolha]} são: \n";
foreach($numeros[$gameEscolha] as $coisas){
    echo "$coisas\n";
}

echo'quantos dezenas  tu deseja apostar?';
$quantosNumeros =trim(fgets(STDIN));

$ultimoNum = count($numeros[$gameEscolha]) - 1;

if($numeros[$gameEscolha][0] > $quantosNumeros or $numeros[$gameEscolha][$ultimoNum] < $quantosNumeros){
    echo "caracter invalido!!!";
}else{
    for ($i=1; $i <= $quantApostas; $i++) {
        echo "A sua {$i}ª aposta é :\n";
        sorteado($gameEscolha, $quantosNumeros);
        echo "///";
        echo "\n";
    }

    $valores = valor($gameEscolha,$quantosNumeros,$quantApostas);
    echo "voce devera pagar: ";
    echo "R$" ;
    echo number_format($valores, 2, ",", ".");

}

?>
