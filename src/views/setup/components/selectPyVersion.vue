<template>
  <div id="select-py-version">
    <div class="field">
      <label for="python-version-select" class="label"
        >Select Python version:</label
      >
      <div class="control">
        <div class="select">
          <select
            v-model="selectedPythonVersion"
            id="python-version-select"
            @change="clearPyErrorStatus"
          >
            <option v-for="ver in pyVersionList" :key="ver" :value="ver">
              {{ ver }}
            </option>
          </select>
        </div>
      </div>
    </div>
    <p v-if="pyVersionList && pyVersionList[0] === 'Not found'">
      Please install
      <a href="https://www.python.org/downloads">Python</a> and reload this
      window.
    </p>

    <folderOpen
      :propLabel="inputLabel"
      :propModel.sync="manualPythonPath"
      :propMutate="setManualPyPath"
      :openMethod="openPythonPath"
      :onChangeMethod="clearPyErrorStatus"
      v-if="selectedPythonVersion === pyVersionList[pyVersionList.length - 1]"
    />
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import { Action, Mutation, State } from "vuex-class";
import folderOpen from "./folderOpen.vue";

@Component({
  components: {
    folderOpen,
  },
})
export default class SelectPyVersion extends Vue {
  @Action private openPythonPath;
  @Mutation setManualPyPath;
  @Mutation setPyExecErrorStatus;
  @Mutation setSelectedSysPython;
  @State("manualPythonPath") storeManualSysPython: string;
  @State("pathSep") private storePathSep: string;
  @State("pyVersionsList") storePyVersionsList: string[];
  @State("selectedSysPython") storeSelectedPythonVersion: string;

  get winRoot() {
    return this.storePathSep === "\\" ? "C:" : "";
  }

  get inputLabel() {
    return `Enter absolute python executable path to use. Example: ${
      this.winRoot
    }${this.storePathSep}Users${this.storePathSep}name${
      this.storePathSep
    }myPythonFolder${this.storePathSep}python${this.winRoot ? ".exe" : ""}`;
  }

  get pyVersionList() {
    return this.storePyVersionsList;
  }

  get selectedPythonVersion() {
    return this.storeSelectedPythonVersion;
  }
  set selectedPythonVersion(newValue: string) {
    this.setSelectedSysPython(newValue);
  }

  get manualPythonPath() {
    return this.storeManualSysPython;
  }

  public clearPyErrorStatus() {
    this.setPyExecErrorStatus("");
  }
}
</script>

<style scoped>
#select-py-version {
  margin: 0.25em;
}
</style>
