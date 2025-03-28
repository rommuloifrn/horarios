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

</script>

<h1>horarios</h1>

<div>
    {#each grade as dia}
        <div>
            dia
            {#each dia.horarios as horario}
                <div>
                    horario
                </div>
            {/each}
        </div>
    {/each}
</div>
