# Evidências - P2 IHC - Minha Padaria

Este documento descreve **o que foi feito** em cada questão e **justifica o porquê** de cada decisão de design tomada, conectando à teoria correspondente.

---

## Questão 1 - Affordance (3,0 pts)

**Conceito aplicado:** Affordance (Norman/Gibson) é a propriedade que um elemento tem de "sugerir visualmente" como ele deve ser usado, sem precisar de instruções.

### Decisões e justificativas

- **Logo clicável no canto superior esquerdo** (`<a class="header-logo">`)
  *Por quê:* É uma **convenção universal da web** — o usuário já espera que clicar no logo o leve à home. Aproveitar essa convenção é affordance cultural pura: o elemento "convida" ao clique porque o usuário já aprendeu o padrão.

- **Menu com botões arredondados que mudam de cor no `:hover`**
  *Por quê:* Links sublinhados azuis (padrão antigo) competem com o design. Botões com `border-radius`, `padding` generoso e mudança de cor no hover indicam claramente "isto é um alvo de clique" — o **feedback visual ao passar o mouse** é o que comunica a affordance.

- **Barra de busca com ícone 🔍 + placeholder "Buscar produtos (ex: pão francês, bolo, café...)" + botão "Buscar"**
  *Por quê:* O ícone de lupa é símbolo universal de busca; o placeholder dá **exemplo concreto** do que digitar (reduz a "tela em branco" e ensina o usuário sem precisar de tutorial). O botão lateral confirma que existe uma ação a executar.

- **Botão CTA "Ver Cardápio ➜" com seta**
  *Por quê:* A seta é um **índice direcional** que sugere "siga por aqui". CTAs com verbo no infinitivo + direção convertem mais porque eliminam ambiguidade sobre o que vai acontecer ao clicar.

- **Cards de produto que se elevam no `:hover` (`transform: translateY(-4px)` + sombra)**
  *Por quê:* A elevação simula o comportamento de um objeto físico que "salta" para frente quando focado. Isso comunica **profundidade e interatividade** — o cartão deixa de parecer estático e passa a parecer um elemento manipulável.

- **Seletor de quantidade `− [qtd] +` em cada item**
  *Por quê:* Em vez de um campo de número solto (que exige digitação), o padrão "stepper" oferece **affordance dupla**: os botões − e + são óbvios para incrementar/decrementar, e o campo central permite digitação direta para quem prefere. Reduz erros e é mais rápido em mobile.

- **Carrinho flutuante (FAB) com badge de contagem**
  *Por quê:* Padrão consagrado em e-commerce (Amazon, iFood). A **posição fixa** garante que o usuário sempre saiba onde está o carrinho; o **badge numérico** fornece feedback constante sem precisar abri-lo. Cor de destaque (laranja) sobre fundo neutro chama atenção sem ser invasivo.

---

## Questão 2 - Heurísticas de Nielsen (3,0 pts)

### A) Visibilidade do status do sistema

- **Barra verde no topo "Aberto agora • Entregas em até 40 min" com bolinha pulsante**
  *Por quê:* O usuário precisa saber **antes de pedir** se a padaria está atendendo. Mostrar esse status no topo (área de maior atenção visual) evita a frustração de montar um pedido e descobrir que está fechada. A animação pulsante reforça "estou vivo, em tempo real".

- **Badge animado no carrinho que pulsa ao adicionar item**
  *Por quê:* Confirma instantaneamente que **a ação foi processada**. Sem esse feedback, o usuário fica em dúvida se o clique funcionou e tende a clicar várias vezes (gerando pedidos duplicados).

- **Toast verde "Nx Item adicionado ✓"**
  *Por quê:* Diferentemente do badge (que mostra o estado), o toast mostra **o que acabou de acontecer**, com o nome e a quantidade. Some sozinho para não exigir ação do usuário. Verde = sucesso (convenção universal).

- **Subtotais e total geral exibidos no carrinho em tempo real**
  *Por quê:* O usuário precisa ver **quanto vai gastar** a cada mudança, sem precisar abrir uma "tela de cálculo". Transparência sobre o estado financeiro do pedido = confiança.

### B) Consistência e padrões

- **Todos os botões de ação primária usam a classe `.btn-primario`** (cor laranja `#d2691e`, mesmo `border-radius`, mesmo hover)
  *Por quê:* O usuário aprende **uma única vez** que "laranja arredondado = botão clicável principal". Aplicar inconsistência (cores diferentes para botões iguais) força o usuário a reaprender em cada tela.

- **Cards de produto com estrutura idêntica:** título → descrição → preço → quantidade → botão
  *Por quê:* Quando os cards têm a mesma ordem visual, o usuário **escaneia mais rápido** (já sabe onde está cada informação). Quebrar essa ordem em alguns cards exigiria releitura.

- **Paleta restrita** (laranja `#d2691e` para ações, verde `#2e7d32` para sucesso/preço, bege/marrom para ambiente)
  *Por quê:* Cada cor carrega um significado consistente em toda a página. Isso reduz a carga cognitiva — o usuário não precisa interpretar uma cor nova a cada seção.

- **Tipografia hierárquica padronizada:** Georgia para títulos (clima artesanal), Arial para corpo (legibilidade).
  *Por quê:* Mistura controlada reforça identidade visual e mantém legibilidade em parágrafos longos.

### C) Prevenção de erros

- **Modal de confirmação antes de finalizar o pedido**
  *Por quê:* "Finalizar" é uma **ação de alto custo de reversão** (gera um pedido real). Pedir confirmação com resumo (qtd e total) dá ao usuário a chance de revisar antes do passo irreversível.

- **Confirmação ao remover item do carrinho (`confirm('Remover este item?')`)**
  *Por quê:* Clicar na lixeira por engano apagaria um item escolhido com cuidado. O custo de uma confirmação extra é baixo; o custo de perder o item é alto.

- **Quantidade mínima 1 e máxima 99** (`min="1" max="99"`) no input numérico
  *Por quê:* Impede valores absurdos (-5, 9999) na origem, em vez de tratar erros depois. **Restringir o input é mais barato que validar a saída.**

- **Botão "Cancelar" sempre presente nos modais**
  *Por quê:* Heurística #3 de Nielsen (controle do usuário): toda ação deve ter "saída de emergência" clara.

- **Input `type="search"`**
  *Por quê:* Habilita o botão nativo de "limpar" do navegador, evitando que o usuário precise apagar caractere por caractere.

### D) Correspondência entre sistema e mundo real

- **Ícones reconhecíveis** (🍩 Doces, 🥐 Salgados, 🎂 Encomendas, 🛒 Carrinho, 📍 endereço, 📞 telefone)
  *Por quê:* Emojis são compreendidos transculturalmente e instantaneamente. Reduzem a leitura de texto e tornam o menu navegável de relance, especialmente para usuários com baixo letramento ou pressa.

- **Linguagem natural em português** ("Adicionar ao pedido", "Minha Conta", "Finalizar pedido")
  *Por quê:* Evita jargão técnico ("submit", "checkout", "ID"). O usuário pensa no mundo dele ("estou fazendo um pedido"), não no mundo do sistema.

- **Preços em formato brasileiro (R$ X,XX com vírgula)**
  *Por quê:* Usar ponto decimal (`R$ 12.90`) parece "estrangeiro" e quebra a expectativa cultural. Pequenos detalhes assim aumentam a sensação de confiança local.

- **Metáfora do carrinho de compras**
  *Por quê:* É uma metáfora física já internalizada — o usuário sabe que pode colocar coisas, tirar, ver o total e "ir ao caixa". Não precisamos inventar uma metáfora nova.

- **"Aberto agora" em vez de "Status: online"**
  *Por quê:* "Aberto" é o termo que o usuário usaria sobre uma padaria física — corresponde à expectativa do mundo real, não à terminologia do sistema.

---

## Questão 3 - Signo Visual (3,0 pts)

**Conceito aplicado:** Semiótica de Peirce — todo signo combina três modos: **ícone** (semelhança), **índice** (causa/relação) e **símbolo** (convenção).

Logo criado em `logo.svg` representa o site da padaria combinando os três tipos de signo de Peirce:

- **ÍCONE** (semelhança): a forma do **pão** desenhada em SVG (elipse marrom com cortes) - parece visualmente com um pão real.
  *Por quê:* O ícone permite reconhecimento **imediato e pré-verbal** — qualquer pessoa, mesmo sem ler "Minha Padaria", identifica o que o estabelecimento vende. É a camada mais universal do signo.

- **ÍNDICE** (relação causal): as **linhas de vapor** subindo do pão indicam que ele acabou de sair do forno (causa→efeito: forno quente → vapor). Os **cortes** no pão são índices das marcas reais feitas pelo padeiro.
  *Por quê:* Vapor não *parece* com pão fresco — ele é **efeito físico** de algo recém-assado. Isso comunica "fresco/quentinho/feito agora" sem precisar escrever a palavra. É um valor de marca (frescor artesanal) transmitido por inferência.

- **SÍMBOLO** (convenção cultural): as **espigas de trigo** nas laterais são convenção universalmente associada à panificação - não parecem com pão, mas culturalmente significam "padaria/cereal".
  *Por quê:* O trigo conecta o estabelecimento a uma **tradição cultural** (agricultura, pão como alimento básico). Esse significado precisa ser aprendido culturalmente — uma criança pequena não associaria espiga a pão. Reforça o posicionamento "tradicional/artesanal" em oposição a "industrializado".

A paleta marrom/dourada também é simbólica (remete a "assado", "artesanal", "tradição").
*Por quê:* Tons quentes ativam associações sensoriais (calor, conforto, comida) e diferenciam de paletas frias (azul/cinza) típicas de fast-food ou tech. A cor reforça o mesmo discurso do logo: artesanal, acolhedor, tradicional.

---