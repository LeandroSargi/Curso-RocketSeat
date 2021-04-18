Tudo sobre GitHub (em construção)


Primeiro de tudo, criar a conta no GitHub.

	Após criar a conta no GitHub, clica no lado direito, na seta que está ao lado da minha foto de perfil.
	Clica em your profile, onde será preenchido o nome e um email público, bio, site, empresa, perfil do 		twitter.



Segundo passo, criando um repositório e um readme.md

	Basta clicar no icone do github e depois em [NEW]
	Normalmente ao seguir essa etapa podemos criar um novo repositório online.
	Mas se eu criar um novo repositório que tenha o nome idêntico ao meu nome de perfil, vai
	ser desbloqueado o repositório especial do github que contém o meu arquivo readme.md
	Este arquivo serve para que eu coloque informações adicionais que serão exibidas no meu perfil do github
	
Terceiro passo, criar chave SSH para conexão segura com computador de trabalho

	Clico na seta que aparece ao lado da minha imagem de perfil no canto superior esquerdo da página do github
	Depois em Settings
	Depois clico em SSH and GPG Keys
	Agora devo ir ao terminal para fazer algumas configurações:
		Com o terminal aberto vou digitar:
			ssh-keygen -t rsa -b 4096 -C "meuemail@meudominio.com"
			Após enviar esse comando, eu posso dar enter para todas as perguntas subsequentes
			e minha chave será criada com sucesso.
		Após criar a chave, eu preciso pegá-la para inserir no meu GitHub.
		Com o terminal aberto vou digitar:
			cd ~/.ssh/
			Dentro desse diretório terei alguns arquivos
			O que eu vou precisar é:
				id_rsa.pub
		Então darei o seguinte comando no terminal:
			cat ~/.ssh/id_rsa.pub
		E copiarei todas as linhas que serão devolvidas pelo terminal
	Volto na página do GitHub e clico em [New SSH Key]
		Dou um nome para a minha máquina e colo o conteúdo da chave retornado pelo terminal,
		no campo onde solicita a chave.
		Chave adicionada com sucesso.
	Agora preciso iniciar o SSH Agent. Com o terminal aberto vou digitar:
		eval "$(ssh-agent -s)"
	Depois preciso adicionar a minha chave SSH ao ssh-agent. Com o terminal aberto vou digitar:
		ssh-add ~/.ssh/id_ed25519
	Pronto, agora minha configuração está feita, posso começar a fazer links entre meus
	repositórios locais e repositórios remotos agora.
	
Quarto passo, criando um link entre um repositório local e um repositório remoto no GitHub

	Vou na minha página do GitHub e crio um novo repositório.
	Entro nesse repositório e clico na guia ssh, onde terá um link para copiar
	
	Vou na minha máquina e crio um novo diretório de trabalho. Com o terminal aberto digito:
		mkdir demo
	Entro no diretório:
		cd demo
	Inicio um novo repositório na pasta criada:
		git init
	Dentro dessa pasta posso iniciar meus trabalhos criando arquivos
	Após feitas as alterações, devo ver o status das mudanças:
		git status
	Adicionar minhas mudanças para que sejam rastreadas as alterações:
		git add . //ponto serve para adicionar tudo
	Commitar minhas mudanças //criar um ponto na história
		git commit -m "meu primeiro commit"
	Agora preciso adicionar meu repositório local ao meu repositorio remoto GitHub:
		git remote add origin "aqui dentro vai o link do repositório setado para o protocolo SSH"
	Repositório adicionado com sucesso
	Agora preciso transformar meu branch principal do repositório local chamado "master" para
	"main" conforme configurações atuais do GitHub
		git branch -M main
	Agora vou "empurrar" meu repositório local para o meu GitHub
		git push -u origin main
		Como é a primeira vez que faço a conexão, preciso liberar digitando:
			yes
		Conexão realizada com sucesso
		
Quinto passo, modificando arquivos locais e enviando para o repositório remoto

	Basta entrar no repositorio local e fazer as alterações desejadas.
	Se não tiver nada para alterar. Crie um arquivo demo.md e coloque alguma frase dentro para fazer o teste
	Preciso colocar o arquivo na staged area e commitar (o comando abaixo só serve para novos arquivos)
		git add -am "meu segundo commit"
	Agora vou "empurrar" o arquivo para o GitHub, como já está tudo configurado, basta digitar
		git push

Sexto passo, modificando arquivos remotos e puxando para o repositório local

	Se por acaso você entrou no GitHub, alterou algum arquivo do seu repositório e commitou online
	Se eu entrar no git e digitar:
		git log --oneline
	Ele não vai encontrar o commit que fiz online
	Para que meu git esteja soncronizado com o repositório remoto, preciso "puxar" essas alterações com:
		git pull
	Logo após estará tudo sincronizado
	
	
Sétimo passo, corrigindo conflitos de merge

	Primeiramente devo entrar no meu repositório local e verificar se está tudo correto:
		git status
	Após isso posso "puxar" minhas modificações do repositório remoto para o local:
		git pull
	Ao dar o comando acima, o git me retorna um aviso sobre 3 possibilidades de configuração de merge
	Devo escolher a opção padrão, digitando-a no terminal:
		git config --global pull.rebase false
	Nos próximos git pull estará tudo configuradoe não precisarei fazer isso novamente
	
	Agora para realizar este passo, estaremos simulando um erro muito comum para usuários de Git e GiHub
	Digamos que estou longe da minha máquina e desejo fazer uma alteração online em um arquivo.
	Entro no site do GitHub, faço a alteração, o commit e tudo ok.
	Porém chego em casa e esqueço de dar um git pull para "puxar" as atualizações.
	Alterei o meu aruivo localmente de outra forma, com outras informações digitadas.
	Segui o fluxo naturalmente com git add e git commit, mas antes de "empurar" as modificações,
	vou "puxar" as atualizações do repositório remoto:
		git pull
	Nesse momento, vou receber uma mensagem de conflito de merge no terminal, o meu git não conseguiu
	fazer o merge automático dos arquivos.
	Agora devo entrar no arquivo readme.md e fazer manualmente as alterações:
		nano readme.md
	Vai abrir um terminal, comparando as alterações dos arquivos
	A maneira mais simples de resolver este problema, é abrindo o arquivo contendo o conflito
	no visual studio code.
	O visual studio code por sua vez, me mostra o arquivo de forma mais clara, faço a escolha
	de qual linha desejo manter e clico em salvar.
	O visual studio code se encarregará do restante.
	O que eu precisarei agora é sair do visual studio code, ir para o terminal e dar um commit.
	Após o commit vem o seguinte:
		git pull
		git push
	E pronto, conflito resolvido
	
	
	




Curiosidades sobre o GitHub

	 - Toda vez que eu edito algum arquivo de repositório de terceiros, automaticamente o GitHub cria um fork
	 do repositório em questão, e copia esse fork para o meu perfil. Dentro do meu perfil terei então, um 		repositório
	 com o mesmo nome do repositório do qual estou fazendo uma colaboração
	 
	 - Quando eu gostar de algum código ou projeto no GitHub, posso dar estrelas, eles ficarão
	 salvos como favoritos para eu poder olhar mais tarde
	 
	 - Toda vez que eu der git clone em um repositório do GitHub, os arquivos vão parar no meu
	 diretório atual, basta dar um ls no terminal para localizar
	 
	 - No GitHub, posso fazer pesquisas setando globalmente (para buscar arquivos em todo o GitHub)
	 ou localmente (pesquisar somente dentro dos meus repositórios)
