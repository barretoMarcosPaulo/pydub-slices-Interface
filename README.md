

# Interface para a utilização da biblioteca *__pydud__*  

## 1. Descrição

O projeto consiste em uma interface para a utilização da biblioteca *__pydub__* a fim de facilitar e automatizar o processo de cortes em arquivos de áudio. Dado um diretório o programa é capaz de realizar o máximo de cortes possíveis em uma determinada faixa de tempo. Cada corte gerado é renomeado de acordo com o nome do arquivo original e exportado para um novo diretório automaticamente.

## 2. Dependências

O projeto possui somente uma dependência que é a biblioteca *__pudub__*  do python. A instalação da mesma é feita através do *__pip3__*:

        pip3 install pydub

## 3. Utilização da interface

A utilização da interface é bastante simples, o primeiro passo consiste em instanciar um novo objeto da classe *__AudioSplit__* e informar quatro parâmetros obrigatórios:

1. Diretório de origem(onde os arquivos de audio estão)
2. Diretório de de destino(onde os cortes do audio original serão armazenados)
3. O nome da classe de audio (Um nome para definir o conjunto de audios, ou tipo etc.)
4. Duração em milisegundos dos novos audios que serão gerados 

Exemplo:

    audiosDosCachorros = AudioSplit("audios/latidos" , "audios/latidos_1_min" , "Latidos" , 60000)

Quando um novo objeto é criado todos os audios já são carregados automaticamente em uma lista de objetos da classe *__AudioLoad__*, onde várias informações sobre cada arquivo são guardadas. No próximo tópico será descrito os atributos e métodos de cada uma das classes do projeto.

O segundo passo é iniciar o processo de separação dos audios que é simples. Para iniciar o processo chame o método *__generate_splits__* e aguarde até ser notificado que o processo foi finalizado. Aproveitando o exemplo acima:

    audiosDosCachorros.generate_splits()

E pronto, todos os audios wav contidos na pasta informada foram cortados em "fatias" de 1 minuto(60000 milisegundos) ou até menos, dependendo da duração do audio, por exemplo em um wav de 9:45 minutos quando cortados em fatias de 1 minuto serão gerados 10 novos audios onde o ultimo terá a duração de 45 segundos.


## 4. Métodos e atributos da classe AudioSplit

A classe *__AudioSplit__* é a nossa classe principal e portanto so precisamos instanciar objetos dela. A *__AudioSplit__* contém os seguites atributos:

Atributos

1. *folder_with_files*  (Guarda o diretório onde os arquivos estão)
2. *folder_destination* (Guarda o diretório onde serão armazenados todas as fatias dos audios)
3. *time_duration* (Duração em milisegundos de cada fatia a ser gerada)
4. *class_name* (apenas um nome para definir o conjunto de audios)
5. *audios_segments* (lista com todos os audios carregados, cada audio é um objeto da classe *__AudioLoad__*)

Metódos

1. *generate_splits*  (Gera todos os splits dos audios)
2. *get_files_in_folder* (Carrega todos os arquivos wav do diretório informado)

## 5. Métodos e atributos da classe AudioLoad

A função da classe *__AudioLoad__* é agrupar o máximo de informações possíveis sobre um determinado arquivo, afim de poder ser utilazada na classe anterios para gerar uma lista de todos os arquivos do diretório.  

Atributos

1. *file*  (Armazena o caminho do audio informado)
2. *name* (Armazena o nome do arquivo sem a extensão .wav)
3. *audio_object* (Armazena o objeto da biblioteca pydub para o audio atual)
4. *time_in_seconds* (Duração do audio em segundos)
5. *time_in_miliseconds* (Duração do audio em milisegundos)
5. *number_of_slices* (Quantidade de novos audios que podem ser gerados dado a duração de cada "fatia")

Metódos

1. *get_name_file*  (Retorna o nome do arquivo a partir do caminho informado)
2. *get_number_slices* (Retorna a quantidade de fatias possíveis para o audio)
