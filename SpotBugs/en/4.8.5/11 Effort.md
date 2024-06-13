[TOC]

Effort value adjusts internal flags of SpotBugs, to reduce computation cost by lowering the prediction.

The default effort configuration is same with `more`.

<table class="docutils align-default">
  <thead>
    <tr class="row-odd">
      <th class="head" rowspan="2">
        <p>Flags in FindBugs.java</p>
      </th>
      <th class="head" rowspan="2">
        <p>Description</p>
      </th>
      <th class="head" colspan="4">
        <p>Effort Level</p>
      </th>
    </tr>
    <tr class="row-even">
      <th class="head">
        <p>min</p>
      </th>
      <th class="head">
        <p>less</p>
      </th>
      <th class="head">
        <p>more</p>
      </th>
      <th class="head">
        <p>max</p>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr class="row-odd">
      <td>
        <p>Accurate Exceptions</p>
      </td>
      <td>
        <p>Determine (1) what exceptions can be thrown on exception edges, (2) which,catch blocks are reachable, and (3) which exception edges carry only, “implicit” runtime exceptions.</p>
      </td>
      <td></td>
      <td>
        <p>✔</p>
      </td>
      <td>
        <p>✔</p>
      </td>
      <td>
        <p>✔</p>
      </td>
    </tr>
    <tr class="row-even">
      <td>
        <p>Model Instanceof</p>
      </td>
      <td>
        <p>Model the effect of instanceof checks in type analysis</p>
      </td>
      <td></td>
      <td>
        <p>✔</p>
      </td>
      <td>
        <p>✔</p>
      </td>
      <td>
        <p>✔</p>
      </td>
    </tr>
    <tr class="row-odd">
      <td>
        <p>Track Guaranteed Value Derefs in Null Pointer Analysis</p>
      </td>
      <td>
        <p>In the null pointer analysis, track null values that are guaranteed to be, dereferenced on some (non-implicit-exception) path.</p>
      </td>
      <td></td>
      <td></td>
      <td>
        <p>✔</p>
      </td>
      <td>
        <p>✔</p>
      </td>
    </tr>
    <tr class="row-even">
      <td>
        <p>Track Value Numbers in Null Pointer Analysis</p>
      </td>
      <td>
        <p>In the null pointer analysis, track value numbers that are known to be, null. This allows us to not lose track of null values that are not, currently in the stack frame but might be in a heap location where the, value is recoverable by redundant load elimination or forward, substitution.</p>
      </td>
      <td></td>
      <td></td>
      <td>
        <p>✔</p>
      </td>
      <td>
        <p>✔</p>
      </td>
    </tr>
    <tr class="row-odd">
      <td>
        <p>Interprocedural Analysis</p>
      </td>
      <td>
        <p>Enable interprocedural analysis for application classes.</p>
      </td>
      <td></td>
      <td></td>
      <td>
        <p>✔</p>
      </td>
      <td>
        <p>✔</p>
      </td>
    </tr>
    <tr class="row-even">
      <td>
        <p>Interprocedural Analysis of Referenced Classes</p>
      </td>
      <td>
        <p>Enable interprocedural analysis for referenced classes (non-application classes).</p>
      </td>
      <td></td>
      <td></td>
      <td></td>
      <td>
        <p>✔</p>
      </td>
    </tr>
    <tr class="row-odd">
      <td>
        <p>Conserve Space</p>
      </td>
      <td>
        <p>Try to conserve space at the expense of precision. e.g. Prune unconditional exception thrower edges for control flow graph analysis, to reduce memory footprint.</p>
      </td>
      <td>
        <p>✔</p>
      </td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr class="row-even">
      <td>
        <p>Skip Huge Methods</p>
      </td>
      <td>
        <p>Skip method analysis if length of its bytecode is too long (6,000).</p>
      </td>
      <td>
        <p>✔</p>
      </td>
      <td>
        <p>✔</p>
      </td>
      <td>
        <p>✔</p>
      </td>
      <td></td>
    </tr>
  </tbody>
</table>
