# Painel do Time

Painel para o líder medir o desempenho da equipe dele.

É um sistema **separado** do painel de indicadores das lideranças: site próprio,
senha própria e banco de dados próprio. Quem entra aqui não enxerga as avaliações
das lideranças, e vice-versa.

---

## Estrutura

```
index.html
netlify.toml
package.json
netlify/functions/dados.mjs
```

---

## Publicar

Abra o terminal dentro desta pasta e rode:

```
npx netlify-cli deploy --prod
```

Escolha **Create & configure a new project** — este é um site novo, não o mesmo
do painel das lideranças. Dê um nome diferente, por exemplo `painel-time-orion`.

### A senha, que é obrigatória

Sem senha, qualquer pessoa com o endereço vê nomes, fotos e desempenho da equipe.

1. No Netlify, dentro deste novo site: **Site configuration → Environment
   variables → Add a variable**
2. Chave `SENHA_PAINEL`, valor: uma senha **diferente** da do outro painel
3. **Deploys → Trigger deploy → Deploy site**

Usar senhas diferentes é o que mantém os dois sistemas separados de verdade.

---

## O que está em aberto

Diferente do painel das lideranças, aqui nada vem pronto. O líder monta.

**Cargos** — criados na aba Indicadores. Cada cargo tem a própria lista de
indicadores. Dá para renomear e excluir a qualquer momento.

**Pessoas** — cadastradas na aba Equipe com nome, cargo e unidade. A unidade é
texto livre, e o painel sugere as que você já usou.

**Indicadores** — nome, dica, forma de apuração, meta, unidade, forma de
pagamento e peso. Dá para criar quantos quiser e excluir os que não servem.

Um cargo novo nasce com dois indicadores de exemplo, Faltas e Atrasos, só para
você ter de onde partir. Pode apagar os dois.

---

## As três formas de pontuar

**Limite** — a meta é o teto tolerado, e a nota cai conforme se consome a margem.
Com limite de 4 atrasos: nenhum atraso dá 100%, 1 dá 75%, 2 dá 50%, 4 dá zero.

**Alvo** — a meta é o que se quer atingir. Quanto maior melhor dá o que alcançou
da meta: meta de 12 pedidos por hora com 9 feitos dá 75%. Quanto menor melhor dá
100% na meta e zero no dobro dela.

**Tudo ou nada** — 100% se bater, zero se não bater.

---

## Apuração

**Soma** para contagens, como faltas e atrasos. **Média** para percentuais e
tempos. **Último** para números que já vêm acumulados no mês — vale o lançamento
mais recente, não a média das semanas.

**Indicador sem dado no mês sai da conta.** Ninguém é penalizado por medição que
não aconteceu.

---

## Com ou sem bônus

Cada cargo tem um campo **Bônus deste cargo**.

Deixando em **0**, o painel mede só desempenho: tudo aparece em percentual, sem
valores em reais. É o modo esperado para a maioria dos times.

Colocando um valor, o painel passa a mostrar quanto cada um conquistou em reais,
e os pesos dos indicadores são ajustados para que o mês perfeito pague exatamente
esse valor, nunca mais.

Com bônus em 0, os valores dos indicadores funcionam como peso: um indicador com
o dobro do valor pesa o dobro na nota.

---

## As abas

**Equipe** — cadastro, foto e quais indicadores valem para cada pessoa.

**Indicadores** — cargos, indicadores, metas, pesos e bônus.

**Apuração** — abre a semana, de segunda a domingo, e lança os números. O
formulário se monta sozinho a partir dos indicadores de cada cargo.

**Desempenho** — gráfico ao longo do mês, comparativo e o detalhe por pessoa,
indicador por indicador.

**Destaque do mês** — o primeiro colocado de cada cargo, com foto, pronto para
imprimir.

---

## Se algo der errado

**Página abre vazia dizendo "Acesso não liberado"** — a função não subiu. Confira
se `netlify/functions/dados.mjs` está no lugar.

**Pede senha e não aceita** — confira a variável `SENHA_PAINEL` no Netlify e
republique depois de criá-la.

**Alguém sumiu do ranking** — provavelmente está sem nenhum indicador lançado no
mês, ou o cargo dela foi excluído. Confira na aba Equipe.
