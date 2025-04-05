<script lang="ts">
    import type { Dia } from "../models/dia";
    import html2canvaspro from 'html2canvas-pro';

    let grade: Dia[] = $state([])

    let qtdHorarios = 3
    let qtdDias = 5

    montaGrade()

    function montaGrade() {
        for (let i=0; i<qtdDias; i++)
            grade.push({'horarios':[]})
        
        for (var dia of grade)
            for (let i=0; i<qtdHorarios; i++)
                dia.horarios.push({'cor':0, 'local':'', 'materia':''})
    }
    
    function baixaImagem() {

        
        let grade: HTMLElement | null = document.getElementById('grade')

        html2canvaspro(grade!).then(function(canvas) {
            let link = canvas.toDataURL()
            
            let el: any = document.createElement("a")
            el.href = link;
            el.download = 'grade gerada por horarios.png'

            el.click()
        });
    }

</script>

<h1 class="text-3xl">horarios</h1>

<p>
    Salve seus horários, lil bro!
</p>

<button class="bg-ctp-mauve text-ctp-base px-3 py-2 rounded cursor-pointer transition hover:bg-ctp-pink font-semibold" onclick={()=>{baixaImagem()}}>
    baixar
</button>


<div id="grade" class="flex mt-10 w-max bg-ctp-base">
    {#each grade as dia}
    <div class="mr-1">

        dia
        
            
            {#each dia.horarios as horario}
                <div class="bg-ctp-mantle w-28 h-20 mt-1 rounded-md p-3">
                    <input class="w-full font-medium" type="text" bind:value={horario.materia} name="" id="">
                    <input class="w-full text-ctp-subtext1" type="text" bind:value={horario.local} name="" id="">
                </div>
            {/each}
        
    </div>
    {/each}
</div>

