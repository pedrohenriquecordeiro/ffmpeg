## Listar as Streams

Para listar as streams (faixas de vídeo, áudio e legendas) de um arquivo de mídia, você pode usar o seguinte comando no ffmpeg:

```shell
input_file="nome_video.mkv"
ffmpeg -i "$input_file"
```
Procure no retorno do comando a lista de Streams.


## Extrair Legenda

```shell

input_file="meu_video.mp4"
output_file="${file%.*}.srt"

ffmpeg -i "$file" -c copy -map 0:s:0 "$output"

```

Este comando utiliza o **FFmpeg** para extrair legendas de um arquivo de vídeo e salvá-las em um arquivo separado no formato .

### 1) ffmpeg

- Chama o programa FFmpeg, que é uma ferramenta de manipulação de mídia (áudio, vídeo e legendas).
- O FFmpeg é capaz de converter, extrair, compactar e manipular arquivos multimídia.

### 2) -i "$file"

- -i indica o arquivo de entrada.
- "$file" é a variável que contém o nome do arquivo de vídeo.


### 3) -c copy

- ```-c``` significa “codec”, que define como os dados serão processados.
- ```copy``` diz ao **FFmpeg** para não reencodar a legenda, apenas copiá-la para o novo arquivo.
- Isso evita perda de qualidade e torna o processo mais rápido.


### 4) -map 0:s:0

- ```-map```: Seleciona quais faixas (streams) do arquivo serão extraídas.
- ```0```: Refere-se ao primeiro arquivo de entrada (0 significa “arquivo original”).
- ```s```: Especifica que queremos legendas (subtitles).
- ```0```: Refere-se à primeira faixa de legendas encontrada.

  
#### Exemplo prático

Se o arquivo video.mp4 contiver:

```
Stream #0:0 → Vídeo
Stream #0:1 → Áudio Inglês
Stream #0:2 → Áudio Português
Stream #0:3 → Legenda Inglês
Stream #0:4 → Legenda Português
```

- ```-map 0:s:0``` escolheria Legenda Inglês.
- ```-map 0:s:1``` escolheria Legenda Português.


### 5) "$output"

- Define o nome do arquivo de saída.
- "$output" é uma variável que contém o nome do novo arquivo (a legenda extraída).







### ffmpeg

O programa principal utilizado no comando é o ffmpeg, que serve para manipular e processar vídeos, áudios e legendas.

Agora, vamos destrinchar os argumentos usados no ffmpeg.

1 - ```-i "$i"```
- Significa: Esse é o arquivo de entrada que o ffmpeg vai processar.
- $i: É o nome do arquivo atual do loop.
- Exemplo: Se o arquivo atual for video1.mp4, o comando vai ser:

2 - *ffmpeg -i "video1.mp4"*

```-c copy```
- Significa: Copia os dados sem reencodá-los.
- Isso é usado porque reencodar as legendas não é necessário — queremos apenas extraí-las como estão, para economizar tempo.

3 - ```-map 0:s:0```
- Significa: Escolhe especificamente a primeira faixa de legendas do arquivo de entrada.
- Vamos dividir isso em partes:
	- 0: Refere-se ao primeiro arquivo de entrada. Como só temos 1 arquivo, ele é o arquivo atual.
	- s: Refere-se a legendas (subtitles).
	- 0: Refere-se à primeira faixa de legendas.
- Exemplo: Se o arquivo video1.mp4 tiver várias faixas, como:
	- Vídeo
	- Áudio em Inglês
	- Áudio em Português
	- Legenda 1 (Inglês)
	- Legenda 2 (Português)
   
Esse comando vai pegar a **Legenda 1**.

4 - ```${i%.*}.srt```
- Significa: Define o nome do arquivo de saída.
- ${i%.*}: Remove a extensão do arquivo original.

#### Exemplo: Se o arquivo for video1.mp4, o resultado será video1.
- .srt: Adiciona a extensão .srt, que é o formato de arquivo de legendas.
- Resultado:
Se o arquivo original for video1.mp4, o arquivo de saída será video1.srt.

### Notas Importantes
- Se não houver legendas no vídeo: O comando pode falhar ou gerar um arquivo .srt vazio.
- Certifique-se de ter ffmpeg instalado:
	- Você pode instalar usando um gerenciador de pacotes, como apt no Linux ou brew no macOS.
- Se houver múltiplas legendas: Esse comando pega apenas a primeira. Para pegar outra faixa, você pode ajustar o número após ```0:s:```, como ```0:s:1``` para a segunda faixa.


### Exemplo Completo:

Imagine que temos os arquivos:
	- movie1.mp4
	- movie2.mkv

O comando expandido será:
```
ffmpeg -i "movie1.mp4" -c copy -map 0:s:0 "movie1.srt"
ffmpeg -i "movie2.mkv" -c copy -map 0:s:0 "movie2.srt"
```
Esse comando:
1 - Pega o arquivo de vídeo.
2 - Extrai a primeira faixa de legendas (se existir).
3 - Salva as legendas como um arquivo separado com a extensão .srt.


