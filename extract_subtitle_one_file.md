## Listar as Streams

Para listar as streams (faixas de vídeo, áudio e legendas) de um arquivo de mídia, você pode usar o seguinte comando no ffmpeg:

```shell
input_file="nome_video.mkv"
ffmpeg -i "$input_file"
```
Procure no retorno do comando a lista de Streams.


## Extrair Legenda

### Formato srt 
( Stream #0:2(eng): Subtitle: subrip (srt) (default) )
```shell

input_file="meu_video.mp4"
ffmpeg -i "$input_file" -c copy -map 0:s:0 "${input_file%.*}.srt"

```

### Formato ASS
(Stream #0:2(eng): Subtitle: ass (ssa))
```
  ffmpeg -i "Anora 2024 1080p WEB-DL HEVC x265 5.1 BONE.mkv" -map 0:2 -c:s copy english_subs.ass
```

Este comando utiliza o **FFmpeg** para extrair legendas de um arquivo de vídeo e salvá-las em um arquivo separado no formato .

### Explicação
#### Formato SRT
##### 1) ffmpeg

- Chama o programa FFmpeg, que é uma ferramenta de manipulação de mídia (áudio, vídeo e legendas).
- O FFmpeg é capaz de converter, extrair, compactar e manipular arquivos multimídia.

##### 2) -i "$file"

- -i indica o arquivo de entrada.
- "$file" é a variável que contém o nome do arquivo de vídeo.


##### 3) -c copy

- ```-c``` significa “codec”, que define como os dados serão processados.
- ```copy``` diz ao **FFmpeg** para não reencodar a legenda, apenas copiá-la para o novo arquivo.
- Isso evita perda de qualidade e torna o processo mais rápido.


##### 4) -map 0:s:0

- ```-map```: Seleciona quais faixas (streams) do arquivo serão extraídas.
- ```0```: Refere-se ao primeiro arquivo de entrada (0 significa “arquivo original”).
- ```s```: Especifica que queremos legendas (subtitles).
- ```0```: Refere-se à primeira faixa de legendas encontrada.

  
### Exemplo prático

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






