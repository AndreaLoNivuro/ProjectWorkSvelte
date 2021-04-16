<script>
    import { onMount } from 'svelte';
    import SvelteTable from "svelte-table";

    import '../styleFile/entrateuscite.css';

    import Api from '../Api.js';

    let rows = []
    let columns = []

    function clickrow() {
        alert(1)
    }

    function myFunction(numCol) {

        var x = document.getElementById("prova");
        var btn = document.createElement("BUTTON");
        btn.innerHTML = "MODIFICA"; 
        columns[numCol].appendChild(btn);
    }

    onMount(async () => {
		const response = await Api.get('/movement/findAll')

        rows = response.result

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
                filterValue: v => Math.floor(v.amount / 10)
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
            },
            // {
			//     title: "button",
            //     value: () => myFunction(4),
			
		    // }
        ];
	});
    
</script>

<div id="prova">
    {#if rows.length > 0 && columns.length > 0}
        <SvelteTable columns="{columns}" rows="{rows}" clickRow={clickrow()}></SvelteTable>
    {/if}
</div>

<style>
	/* :global(tbody) {
		height:250px;
		overflow:auto;
		display: block;
	} */
	:global(thead, tbody tr) {
		display:table;
		width:100%;
		table-layout:fixed;
	}
	:global(th:nth-child(1), td:nth-child(1)) {
		width: 10%;
	}
    :global(th:nth-child(2), td:nth-child(2)) {
		width: 20%;
	}
    :global(th:nth-child(3), td:nth-child(3)) {
		width: 50%;
	}
    :global(th:nth-child(4), td:nth-child(4)) {
		width: 10%;
	}
    :global(th:nth-child(5), td:nth-child(5)) {
		width: 10%;
	}
</style>