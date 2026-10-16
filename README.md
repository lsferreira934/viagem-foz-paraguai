# Rolê Tríplice Fronteira

Site da viagem de 5 amigos a Foz do Iguaçu, Ciudad del Este e Puerto Iguazú (08 a 12/10/2026), de carro saindo de São José dos Campos. Publicado no GitHub Pages: https://lsferreira934.github.io/viagem-foz-paraguai/

A viagem terminou. Hoje o site serve para conferir as contas: abre direto na aba **Contas**.

## Arquivos

| Arquivo | O que é |
|---|---|
| `index.html` | Site principal, tudo inline (HTML, CSS, JS). Abas: Contas, Roteiro, Compras, Rotas, Infos. |
| `completo.html` | Versão longa do guia, com fotos e mapas. |
| `contas.json` | Gastos em comum, divisão e pagamentos. Lido pela aba Contas. |
| `dados.json` | Preços do Paraguai. Atualizado de hora em hora pelo crawler da VPS. |
| `img/pedagios/00.jpg` a `34.jpg` | Cupons de pedágio, na ordem da viagem (00 = Osasco). |
| `img/cupons/` | Cupons de combustível, mercado, restaurante, estacionamentos e o contrato da Unidas (CPF, CNH e telefone tarjados). |
| `img/*.jpg` | Fotos do roteiro. |

## Aba Contas

Renderizada por `renderContas()` em `index.html`. Ordem na tela: extrato de cada pessoa (toca no nome e abre), quadros de total e média, gastos em comum com os comprovantes.

### `contas.json`

```json
{
 "pessoas": ["Leandro", "Cíntia", "Emerson", "Alice", "Alisson"],
 "nucleos": [{"nome": "Leandro e Cíntia", "membros": ["Leandro", "Cíntia"]}],
 "gastos": [{
   "desc": "Pedágios (ida e volta, 36 passagens)",
   "valor": 463.40,
   "pagou": "Leandro",
   "dividir": "todos",
   "ok": true,
   "fonte": "34 cupons + fatura do cartão",
   "itens": [{"d": "08/10 21:12", "local": "Itapevi", "v": 9.80, "img": "img/pedagios/01.jpg", "obs": "opcional"}]
 }],
 "pagamentos": [{"de": "Alice", "para": "Leandro", "valor": 470.00, "obs": "opcional"}],
 "faltam": []
}
```

- `dividir`: `"todos"` (divide pelas 5 pessoas) ou uma lista de nomes, por exemplo `["Leandro", "Alisson", "Emerson"]`.
- `itens`: opcional. Vira o botão "Ver os N lançamentos e cupons" (ou "Ver o comprovante" quando tem um só). A soma dos `v` deve bater com `valor`.
- `pagamentos`: acertos já feitos entre as pessoas. Somam no "pagou" de quem pagou e descontam de quem recebeu. Saldo zerado aparece como "quitado ✓".
- `faltam`: lista do aviso "Falta lançar". Vazia mostra "Tudo lançado".
- Quando algum gasto não é dividido por todos, os quadros do topo viram "Média por pessoa" e "Média por casal".

### Lançar ou corrigir um gasto

1. Editar `contas.json` (reduzir a foto do cupom com `sips -Z 1100 -s format jpeg -s formatOptions 70` antes de pôr em `img/`).
2. Conferir local: `python3 -m http.server 8765` e abrir `http://localhost:8765/index.html` (`fetch` não funciona em `file://`).
3. `git pull --rebase` antes do push: a VPS faz commit "Preços atualizados pela VPS" toda hora.
4. O GitHub Pages publica em ~1 minuto, mas o navegador guarda cache por 10 minutos.

Nunca publicar documento pessoal sem tarja (CPF, CNH, telefone) nem comprovante de Pix ou fatura.

## Resultado final das contas (15/10/2026)

Total em comum R$ 4.243,47, tudo pago pelo Leandro. Partes: Leandro, Emerson e Alisson R$ 851,23; Cíntia e Alice R$ 844,89 (o café de domingo foi dividido entre 3). Quitado: Alice pagou R$ 470,00, Alisson R$ 17,78 e a Alice fez um Pix de R$ 2.059,57 em 14/10 cobrindo o restante dos três.

Detalhe da conciliação, decisões e pendências com a Unidas: nota "Fechamento das contas" no Obsidian (`Viagem Paraguai/`).
