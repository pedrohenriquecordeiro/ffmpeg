
# Extrai Legendas de Varios Videos

```shell
for i in name_file ; do ffmpeg -i "$i" -c copy -map 0:s:0 "${i%.*}.srt"; done
```

#### Propósito Geral:
Esse comando faz um loop sobre uma lista de arquivos (provavelmente arquivos de vídeo)) Para cada arquivo, ele usa o programa ffmpeg para extrair a primeira faixa de legendas e salvá-la em um arquivo .srt.



## 1) for i in name_file
- O que significa: Este é o início de um loop.
- O que ele faz: Pega uma lista de arquivos chamada name_file (ou pode ser uma expressão, como *.mp4) e, para cada arquivo dessa lista, ele guarda o nome do arquivo atual na variável i.

#### Exemplo Prático:
Imagine que name_file contém:
```
video1.mp4
video2.mkv
video3.avi
```

O loop será executado 3 vezes, com:
- Na 1ª vez: i = video1.mp4
- Na 2ª vez: i = video2.mkv
- Na 3ª vez: i = video3.avi

## 2) do
- O que significa: Inicia o bloco de comandos que será executado para cada arquivo da lista.

## 3) ffmpeg

O programa principal utilizado no comando é o ffmpeg, que serve para manipular e processar vídeos, áudios e legendas.
- O que está acontecendo aqui: Para cada arquivo no loop, ele executa o ffmpeg para extrair uma faixa de legendas.

Agora, vamos destrinchar os argumentos usados no ffmpeg.

## 4) -i "$i"
Esse é o arquivo de entrada que o ffmpeg vai processar.
- ```$i```: É o nome do arquivo atual do loop.
Exemplo: Se o arquivo atual for video1.mp4, o comando vai ser:
```
ffmpeg -i "video1.mp4"
```

## 5) -c copy
Copia os dados sem reencodá-los.
- Isso é usado porque reencodar as legendas não é necessário — queremos apenas extraí-las como estão, para economizar tempo.

## 6) map 0:s:0
Escolhe especificamente a primeira faixa de legendas do arquivo de entrada.

Vamos dividir isso em partes:
- 0: Refere-se ao primeiro arquivo de entrada) Como só temos 1 arquivo, ele é o arquivo atual.
- s: Refere-se a legendas (subtitles).
- 0: Refere-se à primeira faixa de legendas.

Exemplo: Se o arquivo video1.mp4 tiver várias faixas, como:
```
Vídeo
Áudio em Inglês
Áudio em Português
Legenda 1 (Inglês)
Legenda 2 (Português)
```
Esse comando vai pegar a Legenda 1.

## 7) ${i%.*}.srt
Define o nome do arquivo de saída.
	- ${i%.*}: Remove a extensão do arquivo original.

#### Exemplo
Se o arquivo for video1.mp4, o resultado será video1.
	- .srt: Adiciona a extensão .srt, que é o formato de arquivo de legendas.

#### Resultado:
Se o arquivo original for video1.mp4, o arquivo de saída será video1.srt.

## 7) done
Finaliza o loop. Depois de executar o bloco de comandos para cada arquivo, o loop termina.

## Exemplo Completo:

Imagine que temos os arquivos:
```
movie1.mp4
movie2.mkv
```
O comando expandido será:

```
ffmpeg -i "movie1.mp4" -c copy -map 0:s:0 "movie1.srt"
ffmpeg -i "movie2.mkv" -c copy -map 0:s:0 "movie2.srt"
```

Esse comando:
1)	Pega o arquivo de vídeo.
2)	Extrai a primeira faixa de legendas (se existir).
3)	Salva as legendas como um arquivo separado com a extensão .srt.

### Notas Importantes
- Se não houver legendas no vídeo: O comando pode falhar ou gerar um arquivo .srt vazio.
- Certifique-se de ter ffmpeg instalado: Você pode instalar usando um gerenciador de pacotes, como apt no Linux ou brew no macOS.
- Se houver múltiplas legendas: Esse comando pega apenas a primeira) Para pegar outra faixa, você pode ajustar o número após 0:s:, como 0:s:1 para a segunda faixa.

