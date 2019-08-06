MZBUILD
==========
Build helper para o BananaPKG.  
Automatiza diversas funções na criação de um pacote `.mz`, evitando repetição desnecessária e facilitando manter o pacote em futuras atualizações do mesmo.

*Read this in other languages: [English](README.md), [Português (BR)](README.pt-BR.md).*

Porquê?
----------
Inspirado por projetos como o *Makepkg*, *rpmbuild*, *SlackBuilds*, entre outros, junto a vontade de contribuir para os projetos [BananaPKG](https://bananapkg.github.io/) e [Mazon OS](https://github.com/mazonos/), então surgiu o projeto *mzbuild*.

A construção de um pacote com o BananaPKG é uma tarefa simples, porém acredito que automatizando tarefas repetitivas, que precisam ser feitas a cada nova versão ou *build* (como o *download*, extração e preenchimentos), nos permite focar melhor naquilo que realmente importa.

Receitas
----------
Assim como o `.spec`, `.PKGBUILD`, `.SlackBuild`, aqui também existe um arquivo com a receita a ser seguida, não é obrigatório uma extensão específica, porém é recomendado `.mzb.sh`. Dessa forma fica explícito que se trata de um *shell script*, como também faz referência ao **mzb**uild.

As variáveis do arquivo são muito semelhantes ao do arquivo *desc* do BananaPKG e possuem nomes bem sugestivos, o que acredito que dispense explicações.

O *checksum* para verificar a integridade do *download* pode ser feito usando *md5* (`CHECKSUM_MD5`) ou *sha256* (`CHECKSUM_SHA256`), basta definir o valor da soma na variável referente. Também é possível não utilizar nenhum *checksum* (não recomendado), como também ambos (não faz sentido).

O *array* `makedeps` é um adicional as dependências do pacote, sendo essas necessárias apenas no *compile time*.

Por fim temos as funções executadas em determinados momentos do processo. Atualmente há a função `build()`, executada logo após a extração, deve ser utilizada para a configuração e compilação da aplicação. Enquanto a função `package()` é executada após a `build()` e antes do empacotamento com o BananaPKG, deve ser utilizada para instalar/copiar os arquivos na `bindir` (variável que contém o caminho do diretório correspondente a raiz do pacote).

> Veja exemplos em [mzbuild-packages](https://github.com/joseafga/mzbuild-packages)

Dependências
----------
- bash
- coreutils
- cURL
- polkit
- tar

Instalação
----------
**TODO:** É pretendido fazer um pacote para o mzbuild, assim será facilmente gerenciado com o BananaPKG, porém é desejado que o desenvolvimento esteja um pouco mais avançado.

É possível testar o mzbuild em seu estado atual com o seguinte comando:

    # curl -L 'https://raw.githubusercontent.com/joseafga/mzbuild/master/mzbuild' -o '/usr/bin/mzbuild' && chmod +x '/usr/bin/mzbuild'

> Assegure-se de saber o que está fazendo

Uso
------
    mzbuild [opções] <arquivo.mzb.sh>

As opções disponíveis são:

    --no-download     não faz download
    --force-download  força download mesmo que o arquivo já exista
    -V, --version     exibe versão do mzbuild e sai

Opções para instalar após criar o pacote e verbose já estão nos planos, outras sugestões são bem-vindas.

Licença
------
**Licença MIT**  
Veja o arquivo [LICENSE](LICENSE).
