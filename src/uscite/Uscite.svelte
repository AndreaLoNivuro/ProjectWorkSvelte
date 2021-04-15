<script>
    import { onMount } from 'svelte';
    import SvelteTable from "svelte-table";
    import UsciteChart from "./UsciteChart.svelte";

    import {link} from 'svelte-spa-router'

    import '../styleFile/entrateuscite.css';

    import Api from '../Api.js';

    let rows = []
    let columns = []

    onMount(async () => {
		const response = await Api.get('/movement/findAll')

        rows = response.result.filter(row => {
            if (row.type === "uscita") {
                return row
            }
        })

        columns = [
            {
                key: "amount",
                title: "Importo",
                value: v => v.amount,
                sortable: true,
                filterOptions: rows => {
                // generate groupings of 0-10, 10-20 etc...
                let nums = {};
                rows.forEach(row => {
                    let num = Math.floor(row.amount / 10);
                    if (nums[num] === undefined)
                    nums[num] = { name: `${num * 10} to ${(num + 1) * 10}`, value: num };
                });
                // fix order
                nums = Object.entries(nums)
                    .sort()
                    .reduce((o, [k, v]) => ((o[k] = v), o), {});
                return Object.values(nums);
                },
                filterValue: v => Math.floor(v.amount / 10),
                headerClass: "text-left"
            },
            {
                key: "category",
                title: "Categoria",
                value: v => v.category,
                sortable: true,
                filterOptions: rows => {
                // use first letter of first_name to generate filter
                let letrs = {};
                rows.forEach(row => {
                    let letr = row.category.charAt(0);
                    if (letrs[letr] === undefined)
                    letrs[letr] = {
                        name: `${letr.toUpperCase()}`,
                        value: letr.toLowerCase()
                    };
                });
                // fix order
                letrs = Object.entries(letrs)
                    .sort()
                    .reduce((o, [k, v]) => ((o[k] = v), o), {});
                return Object.values(letrs);
                },
                filterValue: v => v.category.charAt(0).toLowerCase()
            },
            {
                key: "description",
                title: "Descrizione",
                value: v => v.description,
                sortable: true,
                filterOptions: rows => {
                // use first letter of last_name to generate filter
                let letrs = {};
                rows.forEach(row => {
                    let letr = row.description.charAt(0);
                    if (letrs[letr] === undefined)
                    letrs[letr] = {
                        name: `${letr.toUpperCase()}`,
                        value: letr.toLowerCase()
                    };
                });
                // fix order
                letrs = Object.entries(letrs)
                    .sort()
                    .reduce((o, [k, v]) => ((o[k] = v), o), {});
                return Object.values(letrs);
                },
                filterValue: v => v.description.charAt(0).toLowerCase()
            },
            {
                key: "date",
                title: "Data",
                value: v => v.date,
                sortable: true,
            }
        ];
    });
</script>

<div class="grid-container2">
    <div class="button">
      <div class="radius-icon">
        <a href="/" use:link class="btn btn-xs btn-info">
          MOSTRA RIEPILOGO
        </a>
      </div>
        <!-- <button>MOSTRA RIEPILOGO</button> -->
    </div>
    <div class="side fixed">
      <div class="chart titolo">
        <br>Uscite
        <UsciteChart></UsciteChart>
      </div>
      <div class="date">
        <div class="inizio">
            Data inizio
        </div>
        <div class="fine">
            Data fine
        </div>
        <div class="inputInizio">
            <input type="date">
        </div>
        <div class="inputFine">
            <input type="date">
        </div>
      </div>
    </div>
    <div class="table tableWidth">
        <SvelteTable columns="{columns}" rows="{rows}"></SvelteTable>
    </div>
  </div>