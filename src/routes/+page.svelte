<script lang="ts">
    import type { Dia } from "../models/dia";

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

    import html2canvas from 'html2canvas';
    //import ReImg from 'reimg'
    //import 'reimg'
    function baixaImagem() {

        
        let grade: HTMLElement | null = document.getElementById('grade')

        html2canvas(grade!).then(function(canvas) {
            let link = canvas.toDataURL()
            
            let el: any = document.createElement("a")
            el.href = link;
            el.download = 'grade.png'

            el.click()
        });
    }

</script>

<h1 class="text-3xl">horarios</h1>

<p>
    Salve seus horários, lil bro!
</p>

<button onclick={()=>{baixaImagem()}}>
    baixar
</button>


<div id="grade" class="flex mt-10 w-max">
    {#each grade as dia}
    <div class="mr-1">

        dia
        
            
            {#each dia.horarios as horario}
                <div class="bg-zinc-300 w-28 h-20 mt-1 rounded-md p-3">
                    horario
                </div>
            {/each}
        
    </div>
    {/each}
</div>

