<template>
    <layout class-prefix="layout">
        <NumberPad :value.sync="record.amount" @submit="saveRecord"/>
        <Tabs :data-source="recordTypeList" :value.sync=record.type
        />
        <div class="notes">
            <FormItem @update:value="onUpdateNotes" field-name="备注" placeholder="请输入备注信息" :value="record.notes"/>
        </div>
        <tags @update:value="record.tags = $event"/>

    </layout>
</template>

<script lang="ts">
    import Vue from 'vue';
    import NumberPad from '@/components/Money/NumberPad.vue';
    import FormItem from '@/components/Money/FormItem.vue';
    import Tags from '@/components/Money/Tags.vue';
    import {Component} from 'vue-property-decorator';
    import Tabs from '@/components/Tabs.vue';
    import recordTypeList from '@/constants/recordTypeList';


    @Component({
        components: {Tabs, Tags, FormItem, NumberPad},
    })
    export default class Money extends Vue {
        record: RecordItem = {
            tags: [], notes: '', type: '-', amount: 0, createAt: ''
        };

        get recordList() {
            return this.$store.state.recordList;
        }

        recordTypeList = recordTypeList;


        created() {
            this.$store.commit('fetchRecords');
        }


        onUpdateNotes(value: string) {
            this.record.notes = value;
        }

        saveRecord() {
            if (!this.record.tags || this.record.tags.length === 0) {
                return window.alert('请选择至少一个标签');
            }
            this.$store.commit('createRecord', this.record);
            if (this.$store.state.create.createRecordError === null) {
                window.alert('操作成功');
                this.record.notes = '';
            }

        }
    }
</script>

<style lang="scss" scoped>
    ::v-deep .layout-content {
        display: flex;
        flex-direction: column-reverse;
    }

    .notes {
        padding: 12px 0;
    }
</style>
