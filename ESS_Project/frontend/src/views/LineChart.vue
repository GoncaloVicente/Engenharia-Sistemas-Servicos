<script>
    import {Line} from "vue-chartjs";

    export default {
        extends: Line,
        props: ['data', 'labels'],
        mounted() {
            this.renderChart(
                {
                    labels: this.labels,
                    datasets: [
                        {
                            label: "Power Consumed",
                            data: this.data.consumed,
                            backgroundColor: "rgba(255, 0, 0, 0.50)",
                            borderColor: "rgba(255, 0, 0, 0.50)",
                            pointBackgroundColor: "rgba(171, 71, 188, 1)"
                        },
                        {
                            label: "Power Produced",
                            data: this.data.produced,
                            backgroundColor: "rgba(1, 116, 188, 0.50)",
                            borderColor: "rgba(1, 116, 188, 0.50)",
                            pointBackgroundColor: "rgba(171, 71, 188, 1)"
                        }
                    ]
                },
                {
                    responsive: true,
                    maintainAspectRatio: false,
                    title: {
                        display: true,
                        text: "Values in Watts (W)"
                    }
                }
            );
            this.$emit('chart-rendered')
        }
    };
</script>
