# Ola ola ola,

Vou escrever um resumo de como esse repo surgiu e como ele difere do site original. Eu tava vasculhando arquivos velhos da ava e trombei num backup quebrado do site da ava q parece ter existido entre 2001 e 2004. Era um backup do rudi, dentro de uma pasta do Natan, ao lado de uma da rafa, outra do presto e sl mais oq, aquele pedaco tava uma bela bagunca entao eu n tenho certeza da linhagem desse backup mas ao q tudo indica eh um backup de algum momento de 2004.

Apesar de eu estar na Ava nessa epoca, eu tenho zero lembrancas desse site entao eu tava voando meios as cegas sem saber como ele deveria parecer. Olhando no internet archive temos varias capturas entre 2001 e 2004, mas com muita coisa quebrada e faltando (flash, imagens, links externos; tudo isso costuma quebrar e tava quebrado mesmo). Vasculhando os arquivos eu descobri umas aberracoes q eram bem comuns pra epoca, tipo o gif bizarro falando pra fazerem anuncios no site da ava, o popup de propaganda (nem ideia do qq era, a imagem q deveria mostrar parece ser lost media) e uma sessao de login para madrichim onde eles poderiam acessar informacoes dos seus chanichim tipo telefone.

O problema eh q essa porra de site nao conversa com nenhum servidor, vc soh tem um check podre de JS pra ver se vc acertou o login e ai ele te redireciona pra pagina certa. Ou seja, se vc sabe a url, vc pode pular o login e ter acesso a todas as infos pessoais dos chanichim. Pra piorar, TODOS os logins corretos tavam salvos como plain text entao qualquer um poderia ver isso.
Os backups na wayback machine inclusive contem todas as senhas originais, por sorte ela nunca scrapeou as paginas protegidas pelo login. Na versao aqui publicada eu anonimizei tudo pra n ter dor de cabeca mas sinceramente nada disso eh umm problema se vazar hj em dia, senhas tinham as vezes 3 digitos super toscas e os numeros de telefone sao de uma epoca onde celular era raro e telefone fixo tinha 7 digitos. fiz um login falso pra quem quiser brincar: (lyca / 7611) EDIT: eu tb anonimizei todos os nomes de chanich e pais por via das duviads, n quero ninguem me enchendo o saco por isso.

Parte do backup tava corrompido mas juntando com o q tinha na wayback machine deu pra fazer uma reconstrucao bem fiel. 1:1 do original? nao e isso eh provavelmente impossivel pq temos varios arquivos perdidos q ninguem salvou em lugar nenhum q eu pudesse encontrar. Usando ruffle pra emular flash e pushando uns links externos arquivados pela wayback machine (recriei todo o guestbook com ateh mais recados do q no scrap final pq alguns foram deletados entre scraps diferentes), eu consegui reconstruir maior parte das funcionalidades do site. A pagina de registrar um email obviamente nao funciona, mas ta la e o avachat infelizmente parece irrecuperavel seja la o q era aquilo. Algumas das imagens perdidas foram substituidas por um retangulo cinza com um X soh pra ocupar o espaco e a gente saber q tem algo faltando ali (maior exemplo disso eh o iton q n achei nada dele).

Sobre a sessao de fotos, eu n entendi mt bem qq ta faltando ou como q era pra funcionar mas ta semi-funcional. Tem uma porcao de fotos pra ver la, soh n parece ser tudo q ja existiu (midia perdida? codigo buggado? nem ideia)

Pra ter uma experiencia mais proxima do real, vc precisa emular um windows velho com internet explorer 5, convenientemente [o oldwebtoday ja faz isso pra vc](https://oldweb.today/?browser=ie5#20040804195526/http://www.avanhandava.org/frame.htm).
Puxando os scraps da wayback machine vc fica sem varios assets e o site no github nao funciona atraves do oldweb pq githubpages sao obrigatoriamente https e o TLS caga tudo. Tentei subir no gitlab com force https off mas tb n funcionou

Acho q isso eh tudo, espero n estar esquecendo nada. Na seuqencia aqui tenho a explicacao slop da llm q eu usei pra agilizar isso tudo pq eu to com fome e preciso ir terminar de cozinhar minha janta, beijos a todos

-------------------------------------

```
Restore the 2001-2004 site from backup and archive.org

The source is a backup of avanhandava.org as it stood around mid-2004: a
Microsoft FrontPage 5.0 site, frames and all. It did not run as-is. This is
what it took to make it serve again, and what had to be changed.

Encoding
  The pages are windows-1252 and mostly declare no charset. Every static
  host today serves UTF-8, so every accented character in the site would
  have broken. ~140 files re-encoded and their charset meta rewritten.

Missing files, recovered from the Internet Archive
  The backup had lost www/images/ entirely - it appears in none of the
  FTP logs - along with the ecoava/ and iton/ sections and the homepage
  body. archive.org crawled the site in 2001, 2002, 2003 and 2004, so:
    - 59 files pulled back from the nearest capture to mid-2004
    - 18 more recovered by matching filenames elsewhere in the backup
    - 42 still lost; these render as a neutral box at the exact dimensions
      the page declares, so layouts hold instead of collapsing. Where a
      thumbnail of the lost image survived, it is centred in the box.
  Broken same-origin references went from 219 to 11. The 11 that remain
  are files no copy of exists anywhere, archive.org included.

  indice.htm deserves its own note. The backup's only copy was
  indice.htm_TMP.html, a Xara Webstyle working file: it had lost the
  <td background=... rowspan="4"> that anchors the homepage table, wrapped
  three images in "Click to edit" editor anchors, and trailed binary
  rubbish after </html>. Building from it produced a visibly wrong
  homepage. It now comes from the 2004-06-09 capture instead.

  Every other page was checked the same way. Of 77 pages with a capture,
  every one that has a 2004 capture is byte-identical to the backup.

The guestbook
  It lived on livrodevisitas.com.br, which is gone. archive.org held it
  ten entries at a time across sixteen snapshots; those are merged into a
  single local guestbook.htm and the menu now links there. 114 messages,
  January 2000 to March 2004. The book reported 80 entries in 2002 and 103
  by late 2004, so about eleven were deleted at some point and survive only
  in the older snapshots.

Things that worked in 2004 and do not now
  - The Flash intro. Browsers dropped Flash in 2020; Ruffle is vendored
    into the site and plays it. Loaded behind a feature test so browsers
    that cannot use it never fetch it.
  - The date in the header read "de 126". getYear() returned the full
    four-digit year in IE 4+ JScript, which is what this site's audience
    used; every engine since returns year - 1900. Shimmed back.
  - escotismo.htm's title rendered "Esc" small and "autismo" large.
    <big><big><big> stepped to font size 6 in IE, but modern browsers map
    <big> to font-size:larger and multiply by 1.2 per tag. Rewritten to
    the size IE produced.
  - A link that had lost its scheme, and one image referenced with the
    wrong case - fine on Windows in 2004, a 404 on any case-sensitive host.

Removed
  - A dead advertising script and a dead hit counter that only stall page
    load now.
  - FrontPage and WS_FTP working files: .bak, _vti_cnf/, WS_FTP.LOG. They
    serve no purpose online and leak the author's local paths.

Personal data
  The backup contains the group's internal pages, which were never really
  private - the "login" guarding them was a script with the credentials in
  the page source, and the pages behind it were reachable by URL. In this
  published copy:
    - every telephone number is fake, randomised to the same shape as the
      original (184 numbers)
    - every username/password pair is fake (31 pairs)
    - every name in the chanichim roster, children and parents alike, is a
      pseudonym; surnames shared within a family stay shared and the
      pseudonym agrees with the recorded gender (50 rows)
  None of the original values appear anywhere in this repository. Contact
  details elsewhere - the leaders' e-mail list, and the names and addresses
  people chose to post in the guestbook - are unchanged.

Also here
  period.html frames the site at 800x600, the resolution it was drawn for.`

```
