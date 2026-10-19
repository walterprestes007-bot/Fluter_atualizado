Consulta Fácil — Aplicativo Flutter
Aplicativo desenvolvido em Flutter e Dart com navegação entre telas, consultas a serviços públicos, acesso à localização do dispositivo, uso da câmera e galeria e um feed dinâmico inspirado em redes sociais.
Estado do projeto: a tela de login atual é demonstrativa. Ela não autentica e-mail/senha em um servidor: ao tocar em Entrar, o aplicativo abre a tela principal. As telas de consulta e o feed utilizam serviços públicos ou armazenamento local, conforme descrito abaixo.

Índice
- Funcionalidades
- Tecnologias e dependências
- Requisitos
- Como abrir e executar no VS Code
- Navegação do aplicativo
- Feed dinâmico
- Câmera e galeria
- Pasta interna de fotos e persistência
- Consultas e localização
- Estrutura de pastas
- Permissões
- Comandos úteis
- Solução de problemas
- Limitações conhecidas
Funcionalidades
Telas e navegação
- Tela inicial: apresentação do Consulta Fácil e acesso ao fluxo de entrada.
- Login demonstrativo: campos de e-mail e senha e navegação para a tela principal.
- Tela principal: atalhos e menu lateral para abrir as demais funcionalidades.
- Consulta de CEP: pesquisa de endereço a partir de um CEP.
- Consulta de CNPJ: busca informações básicas de uma empresa.
- Conversor de dólar: converte um valor em dólares para reais usando a cotação retornada pela API.
- Minha localização: solicita permissão de localização e mostra latitude e longitude do dispositivo.
- Trabalho: exemplo de navegação inferior com as seções Início, Atividades e Perfil.
- Câmera e Galeria: visualização da câmera, captura de foto, seleção de imagem e pré-visualização.
- Feed Dinâmico: lista de publicações com nomes, imagens, legendas, curtidas, comentários e ação para copiar o resumo da publicação.
- Pasta interna de fotos: grade com as imagens salvas pelas publicações locais; permite abrir uma imagem em tamanho maior.
As telas são abertas pela navegação do aplicativo e podem ser fechadas usando a seta de voltar do sistema ou a seta da barra superior, quando disponível.
Tecnologias e dependências
- Flutter / Dart: interface e lógica do aplicativo.
- Material Design: componentes visuais, botões, listas, menus e caixas de diálogo.
- http: requisições HTTP para os serviços públicos de consulta.
- camera: visualização e captura de imagens usando a câmera do dispositivo.
- image_picker: escolha de fotos da galeria e captura de imagem por meio do seletor do sistema.
- path_provider: obtenção do diretório de documentos privado do aplicativo em Android/iOS.
- shared_preferences: armazenamento local de nomes, metadados de publicações e dados usados pelo armazenamento web.
- geolocator: acesso à localização atual do dispositivo.
As versões declaradas das dependências estão no arquivo pubspec.yaml. A resolução concreta das versões é registrada em pubspec.lock.
Requisitos
1. Flutter instalado e configurado no computador.
2. Uma versão do Dart compatível com a restrição declarada em pubspec.yaml (^3.12.1).
3. Visual Studio Code, com as extensões Flutter e Dart recomendadas.
4. Conexão com a internet para baixar dependências, carregar as imagens de exemplo e consultar APIs externas.
5. Para testar a câmera e o GPS, use preferencialmente um celular físico com as permissões habilitadas ou um emulador configurado com câmera e localização.
Para verificar o ambiente, abra um terminal e execute:
flutter --version
 dart --version
flutter doctor
Se o comando flutter não for reconhecido, instale o Flutter SDK e adicione a pasta bin do SDK ao PATH do sistema antes de continuar.
Como abrir e executar no VS Code
1. Baixe o ZIP do projeto e extraia todos os arquivos para uma pasta local.
2. No VS Code, escolha Arquivo → Abrir Pasta e selecione a pasta project_Fluter (a pasta que contém pubspec.yaml).
3. Abra Terminal → Novo Terminal.
4. Baixe/resolva as dependências:
   flutter pub get
5. Confira os dispositivos que o Flutter encontrou:
   flutter devices
6. Inicie um emulador pelo Android Studio ou conecte um celular com depuração USB habilitada. Em seguida, execute:
   flutter run
Se houver mais de um dispositivo conectado, selecione o dispositivo no VS Code ou informe seu identificador no comando flutter run -d ID_DO_DISPOSITIVO.
Executar no navegador (opcional)
Se o ambiente tiver suporte ao Flutter Web, também é possível executar:
flutter run -d chrome
No navegador, a câmera depende das permissões e das restrições de segurança do browser. O armazenamento web é diferente do armazenamento de arquivos do Android/iOS; consulte Pasta interna de fotos e persistência.
Navegação do aplicativo
O fluxo padrão é:
1. Abra o aplicativo e veja a tela Consulta Fácil.
2. Toque em Entrar para abrir a tela de login.
3. Toque em Entrar na tela de login para acessar a tela principal.
4. Na tela principal, abra uma funcionalidade por um dos atalhos ou pelo menu lateral.
5. Use a navegação de retorno para voltar à tela anterior.
O login é apenas uma demonstração da navegação. Os campos de e-mail e senha não são verificados e não há cadastro, recuperação de senha, sessão ou autenticação por servidor implementados nesta versão.
Feed dinâmico
O feed está implementado em lib/pages/feed_page.dart e oferece uma experiência de listagem de publicações semelhante à de uma rede social.
Como usar
1. Na tela principal, selecione Abrir Feed Dinâmico ou abra Feed Dinâmico pelo menu lateral.
2. A lista mostra publicações de exemplo e as publicações locais já criadas.
3. Use a faixa/lista de nomes para filtrar publicações por pessoa.
4. Use o botão para adicionar um nome à lista. Nomes duplicados são recusados.
5. Para criar uma publicação, selecione o botão de nova publicação e escolha Tirar foto ou Escolher da galeria.
6. Na etapa de preparação, selecione o nome que publicará a imagem e informe uma legenda, se desejar.
7. Confirme a publicação. A imagem será copiada para o armazenamento interno e a publicação será inserida no início do feed.
8. Toque no coração para curtir ou retirar a curtida.
9. Abra os comentários para consultar e inserir comentários locais.
10. A ação Compartilhar copia um resumo textual da publicação para a área de transferência; ela não envia a foto automaticamente para outro aplicativo.
11. Use a opção Pasta interna de fotos para consultar imagens que foram salvas pelas publicações locais.
Dados de exemplo
O feed começa com três publicações e imagens de exemplo hospedadas no Unsplash. Essas imagens precisam de conexão com a internet para carregar. As fotos que o usuário publica são armazenadas localmente pelo aplicativo.
Persistência
- A lista personalizada de nomes fica salva no armazenamento local por shared_preferences.
- Os metadados das publicações criadas no app — autor, caminho da imagem, legenda, curtidas e comentários — ficam salvos localmente.
- Interações feitas nas publicações de exemplo não são armazenadas como publicações locais e podem voltar ao estado inicial quando o aplicativo é reiniciado.
- O feed não utiliza servidor, banco de dados remoto ou sincronização entre dispositivos nesta versão.
Câmera e galeria
A tela lib/pages/camera_gallery_page.dart permite:
- abrir a câmera disponível (priorizando a traseira);
- visualizar a imagem da câmera;
- capturar uma foto;
- escolher uma imagem da galeria;
- pré-visualizar a foto e retornar à câmera para tirar outra;
- tratar situações em que a câmera não está disponível ou a permissão é negada.
Essa tela é independente do fluxo de publicação do feed, mas ambas usam recursos de câmera/galeria. Para publicar a imagem no feed e salvá-la na pasta interna, use o fluxo de nova publicação dentro do próprio feed.
Pasta interna de fotos e persistência
O armazenamento específico por plataforma está dividido em lib/services/:
- Android/iOS: feed_photo_store_io.dart usa path_provider e grava cópias das imagens em uma subpasta chamada fotos_feed dentro do diretório privado de documentos do aplicativo.
- Web: feed_photo_store_web.dart grava os bytes codificados no armazenamento local do navegador com shared_preferences, pois o navegador não fornece um diretório privado comum como os sistemas móveis.
- Fallback: feed_photo_store_stub.dart fornece a implementação alternativa para plataformas sem uma implementação específica.
- Exportação condicional: feed_photo_store.dart seleciona a implementação adequada ao compilar para cada plataforma.
Onde as imagens ficam?
No Android/iOS, a pasta pertence ao espaço privado do app. Em geral, as imagens não aparecem automaticamente no aplicativo Fotos/Galeria do celular. Para consultá-las, abra a tela Pasta interna de fotos no aplicativo.

No navegador, os dados ficam no armazenamento do site/navegador e estão sujeitos às cotas, às configurações de privacidade e à limpeza dos dados do navegador. Isso não cria uma pasta física visível no computador.

Atenção: desinstalar o aplicativo ou limpar os dados do app pode apagar arquivos e informações salvos localmente. Não há backup remoto automático.
Consultas e localização
As telas de consulta dependem de conexão com a internet e de serviços externos. A disponibilidade, os formatos de resposta e as regras desses serviços podem mudar.
Funcionalidade	Serviço utilizado	Dados exibidos
CEP	ViaCEP	Logradouro, bairro, cidade e estado, quando fornecidos pela API.
CNPJ	OpenCNPJ	CNPJ, razão social e nome fantasia, conforme os campos retornados.
Cotação do dólar	AwesomeAPI Economia	Cotação USD/BRL e conversão do valor informado para reais.
Localização	GPS/localização do dispositivo via geolocator	Latitude e longitude, após autorização do usuário.


Os serviços públicos podem limitar requisições ou ficar indisponíveis. Quando não houver conexão ou a API não responder, repita a consulta mais tarde. Evite digitar espaços ou caracteres indevidos nos campos de CEP e CNPJ.
Estrutura de pastas
project_Fluter/
├── lib/
│   ├── main.dart                     # Inicialização do aplicativo
│   ├── localizacao.dart              # Tela e lógica de localização/GPS
│   ├── pages/
│   │   ├── inicial_page.dart         # Tela de boas-vindas
│   │   ├── login_page.dart           # Login demonstrativo
│   │   ├── principal_page.dart       # Atalhos e menu lateral
│   │   ├── cep_page.dart             # Consulta de CEP
│   │   ├── cnpj_page.dart            # Consulta de CNPJ
│   │   ├── dolar_page.dart           # Conversor de dólar
│   │   ├── camera_gallery_page.dart # Câmera e seleção de fotos
│   │   ├── feed_page.dart            # Feed, nomes e pasta de fotos
│   │   └── trabalho_page.dart        # Navegação inferior de exemplo
│   └── services/
│       ├── feed_photo_store.dart     # Exportação condicional
│       ├── feed_photo_store_io.dart  # Arquivos locais Android/iOS
│       ├── feed_photo_store_web.dart # Armazenamento do navegador
│       └── feed_photo_store_stub.dart# Implementação alternativa
├── android/                          # Projeto nativo Android
├── ios/                               # Projeto nativo iOS
├── web/                               # Arquivos do Flutter Web
├── test/                              # Testes automatizados
├── pubspec.yaml                       # Dependências e configuração Dart
├── pubspec.lock                       # Versões resolvidas das dependências
├── analysis_options.yaml              # Regras de análise estática
└── README.md                          # Esta documentação
Permissões
Android
O arquivo android/app/src/main/AndroidManifest.xml contém permissões relacionadas à câmera e localização. Ao usar recursos protegidos, o sistema operacional pode pedir autorização ao usuário.
iOS
O arquivo ios/Runner/Info.plist contém descrições de uso para a câmera e biblioteca de fotos. Se as mensagens de permissão precisarem ser alteradas, edite as descrições nesse arquivo.
Se a permissão for negada
- Abra as configurações do dispositivo.
- Localize o aplicativo e autorize câmera, fotos ou localização conforme a funcionalidade que deseja usar.
- Feche e abra novamente a tela correspondente.
- Para GPS, confirme também que o serviço de localização do aparelho está ativado.
Comandos úteis
Executar a aplicação:
flutter pub get
flutter run
Analisar o código:
flutter analyze
Executar testes automatizados:
flutter test
Listar dispositivos disponíveis:
flutter devices
Limpar arquivos gerados e baixar as dependências novamente (útil em alguns erros de build):
flutter clean
flutter pub get
Gerar um APK de lançamento para Android:
flutter build apk --release
Se a compilação terminar com sucesso, o APK normalmente ficará em build/app/outputs/flutter-apk/app-release.apk dentro da pasta do projeto. A compilação iOS exige macOS com Xcode configurado.
Solução de problemas
flutter ou dart não é reconhecido
O Flutter SDK não está no PATH ou não foi instalado. Configure o SDK e reinicie o terminal/VS Code; confirme com flutter doctor.
Dependências não são baixadas
Confirme a internet e execute flutter pub get novamente. Se o problema persistir, verifique a mensagem completa no terminal e a compatibilidade da versão instalada com pubspec.yaml.
A câmera não abre
- Teste em um celular físico ou emulador com câmera configurada.
- Verifique as permissões nas configurações do sistema.
- Feche outros aplicativos que estejam usando a câmera.
- Tente sair e voltar à tela Câmera e Galeria.
A galeria não retorna uma imagem
Confirme que há uma imagem disponível e que o sistema permitiu o acesso. Cancele o seletor e tente novamente. O comportamento pode variar conforme a versão do Android/iOS e do seletor nativo.
As imagens de exemplo do feed não carregam
As imagens de exemplo são remotas. Verifique a conexão com a internet. As imagens criadas no aparelho e armazenadas pelo app são locais e não dependem do Unsplash.
A pasta interna aparece vazia
Essa pasta mostra as imagens publicadas pelo fluxo do Feed Dinâmico. Tirar ou selecionar uma foto na tela independente Câmera e Galeria não a publica automaticamente no feed. Crie uma publicação dentro do feed para salvar a imagem nessa pasta.
A consulta de CEP, CNPJ ou dólar falha
Verifique a conexão, confira o valor digitado e tente novamente. Como as APIs são externas, falhas temporárias, limites de uso ou mudanças no serviço podem afetar as consultas.
O GPS não retorna a localização
Ative a localização no dispositivo, autorize a permissão e tente novamente em local com sinal suficiente. Em alguns emuladores, é necessário definir uma localização simulada.
Limitações conhecidas
- O login não é uma autenticação real e não protege as telas por usuário.
- O feed é local: não existem contas, servidor, sincronização, notificações ou feed compartilhado entre aparelhos.
- O botão de compartilhar copia texto para a área de transferência; ele não envia automaticamente a foto ou a publicação.
- As imagens de exemplo dependem de internet e são fornecidas por um serviço externo.
- O armazenamento no navegador não é igual a uma pasta do sistema e está sujeito às limitações do navegador.
- A pasta privada Android/iOS é diferente da galeria pública do aparelho.
- O projeto deve ser compilado e testado no ambiente de desenvolvimento alvo; comportamento de câmera e permissões pode variar conforme dispositivo, sistema operacional e versão dos plugins.
Créditos e serviços
- Flutter
- ViaCEP
- OpenCNPJ
- AwesomeAPI Economia
- Unsplash — imagens usadas nas publicações de exemplo.
